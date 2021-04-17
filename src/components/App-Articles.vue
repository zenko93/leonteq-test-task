<template>
  <div class="app-articles">
    <app-article
      v-for="article of articles"
      :key="article.id"
      :article="article"
    />
  </div>
</template>

<script>
import AppArticle from "@/components/App-Article";

export default {
  name: "App-Articles",
  components: { AppArticle },
  props: {
    articles: {
      type: Object,
      required: true,
    },
  },
};
</script>
