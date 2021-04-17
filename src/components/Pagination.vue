<template>
  <div class="pagination">
    <button v-if="page !== 1" type="button" class="mr" @click="page--">
      Previous
    </button>
    <button
      type="button"
      :class="{ 'page-active': page === pageNumber }"
      v-for="pageNumber in pages"
      :key="pageNumber"
      @click="page = pageNumber"
    >
      {{ pageNumber }}
    </button>
    <button v-if="page < pages.length" class="ml" type="button" @click="page++">
      Next
    </button>
  </div>
</template>

<script>
export default {
  name: "Pagination",
  props: {
    articles: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      page: 1,
      perPage: 9,
      pages: [],
    };
  },
  methods: {
    setPages() {
      const numberOfPages = Math.ceil(this.articles.length / this.perPage);
      const pages = [];

      for (let index = 1; index <= numberOfPages; index++) {
        pages.push(index);
      }
      this.pages = pages;
    },
    paginate(posts) {
      let page = this.page;
      let perPage = this.perPage;
      let from = page * perPage - perPage;
      let to = page * perPage;

      return posts.slice(from, to);
    },
  },
  computed: {
    displayedPosts() {
      return this.paginate(this.articles);
    },
  },
  watch: {
    articles() {
      this.setPages();
    },
    displayedPosts() {
      this.$emit("paginatedArticles", this.displayedPosts);
    },
  },
};
</script>

<style scoped>
.pagination {
  margin-top: 24px;
}
.page-active {
  background-color: yellow;
}
.ml {
  margin-left: 16px;
}
.mr {
  margin-right: 16px;
}
</style>
