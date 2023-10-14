<template>
  <div v-if="data">
    <div class="row u-equal-height u-clearfix">
      <card
        v-for="content in data"
        :key="content.id"
        class="col-4 col-medium-2 blog-p-card--post p-card"
        :contents="content"
      ></card>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import card from "./components/Card-Comp.vue";
import "../dist/style.css";
import { useRouter } from "vue-router";
export default {
  name: "App",
  data() {
    return {
      data: null,
    };
  },

  components: {
    card,
  },
  setup() {
    const router = useRouter();
    return { router };
  },
  methods: {
    async getData() {
      const data = await axios.get(
        "https://people.canonical.com/~anthonydillon/wp-json/wp/v2/posts.json"
      );
      this.data = await data.data;
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style></style>
