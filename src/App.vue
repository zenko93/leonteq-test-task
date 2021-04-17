<template>
  <div>
    <h1>List of Books</h1>
    <div class="align-right">
      <title-filter @updateTitle="updateTitle" :title="filterTitle" />
    </div>
    <app-articles :articles="filteredArticles" />
  </div>
</template>

<script>
import AppArticles from "@/components/App-Articles";
import TitleFilter from "@/components/inputs/Title-Filter";

import axios from "axios";

export default {
  name: "App",
  components: { TitleFilter, AppArticles },
  data() {
    return {
      articles: [],
      filterTitle: "",
    };
  },
  computed: {
    filteredArticles() {
      return this.articles.filter((item) =>
        item.title.includes(this.filterTitle)
      );
    },
  },
  async mounted() {
    this.articles = await this.getData();
  },
  methods: {
    async getData() {
      const { data } = await axios(
        "https://fakerestapi.azurewebsites.net/api/v1/Books"
      );
      return data;
    },
    updateTitle(title) {
      this.filterTitle = title;
    },
  },
};
</script>

<style>
.align-right {
  display: flex;
  justify-content: flex-end;
}
</style>
