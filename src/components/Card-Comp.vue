<template>
  <div v-if="contents">
    <div class="p-card__inner-no-margin">
      <h2>Title</h2>
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
      <hr class="u-sv1-no-margin" />

      by
      <a :href="contents._embedded.author[0].link" target="_blank">{{
        contents._embedded.author[0].name
      }}</a>
      on
      {{ formatedDate }}
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
    console.log(this.contents);
  },
  methods: {
    formatDate(date) {
      this.formatedDate = moment(date).utc().format("Do MMMM Y");
      console.log(this.formatedDate);
    },
  },
};
</script>
