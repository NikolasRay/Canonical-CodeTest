<template>
  <div v-if="contents">
    <div class="p-card__inner-no-margin">
      <h4>Cloud And Server</h4>
      <hr class="u-sv1-no-margin" />
      <img
        class="p-card__image"
        alt="fix your images"
        :src="contents.featured_media"
      />
      <h3>
        <a :href="contents.link" target="_blank">{{
          contents.title.rendered
        }}</a>
      </h3>
      <p></p>

      by
      <a :href="contents._embedded.author[0].link" target="_blank">{{
        contents._embedded.author[0].name
      }}</a>
      on
      {{ formatedDate }}
      <hr class="u-sv1-no-margin" />
      <p>Article</p>
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
    };
  },
  mounted() {
    this.formatDate(this.contents.date);
  },
  methods: {
    formatDate(date) {
      this.formatedDate = moment(date).utc().format("Do MMMM Y");
    },
  },
};
</script>
