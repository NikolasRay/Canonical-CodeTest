<template>
  <div v-if="contents" class="card__container">
    <header class="p-card__header">
      <h5 class="p-muted-heading u-no-margin--bottom">
        {{ topic }}
      </h5>
    </header>
    <hr class="u-sv1-no-margin" />
    <div class="blog-p-card__content">
      <div class="u-crop--16-9">
        <a :href="contents.link">
          <div class="lazyload" data-noscript>
            <img
              loading="lazy"
              class="p-card__image"
              alt="fix your images"
              :src="contents.featured_media"
            />
          </div>
        </a>

        <h3 class="p-heading--4">
          <a :href="contents.link" target="_blank"
            >{{ contents.title.rendered }}
          </a>
        </h3>
        <p>
          <em>
            by
            <a :href="contents._embedded.author[0].link" target="_blank">{{
              contents._embedded.author[0].name
            }}</a>
            on
            {{ formatedDate }}
          </em>
        </p>
      </div>
    </div>
    <div class="footer__container">
      <hr class="u-sv1" />
      <p class="blog-p-card__footer">Article</p>
    </div>
  </div>
</template>
<script>
import moment from "moment";

export default {
  props: {
    contents: Object,
  },
  data() {
    return {
      formatedDate: null,
      topic: null,
      topic_id: null,
    };
  },
  mounted() {
    this.formatDate(this.contents.date);
    this.findTopic(this.contents);
  },
  methods: {
    formatDate(date) {
      this.formatedDate = moment(date).utc().format("Do MMMM Y");
    },
    findTopic(contents) {
      this.topic_id = contents.topic[0];

      const termArray = contents._embedded["wp:term"];

      const topicArray = termArray.find(
        (term) => term[0]?.taxonomy === "topic" && term[0]?.id === this.topic_id
      );
      this.topic = topicArray ? topicArray[0]?.name : "Placeholder";
    },
  },
};
</script>
<style scoped></style>
