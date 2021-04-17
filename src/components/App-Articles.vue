<template>
  <div class="app-articles">
    <app-article
      v-for="article of posts"
      :key="article.id"
      :article="article"
    />
    <pagination @paginatedArticles="paginatedArticles" :articles="articles" />
  </div>
</template>

<script>
import AppArticle from "@/components/App-Article";
import Pagination from "@/components/Pagination";

export default {
  name: "App-Articles",
  components: { Pagination, AppArticle },
  props: {
    articles: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    paginatedArticles(articles) {
      this.posts = articles;
    },
  },
};
</script>
