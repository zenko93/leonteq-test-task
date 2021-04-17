<template>
  <div>
    <h2>{{ article.title }}</h2>
    <p>{{ article.description }}</p>
    <div>Publish date: {{ publishDate }}</div>
  </div>
</template>

<script>
export default {
  name: "App-Article",
  props: {
    article: {
      type: Object,
      required: true,
    },
  },
  computed: {
    publishDate() {
      return { ...this.article }.publishDate.slice(0, 10);
    },
  },
};
</script>
