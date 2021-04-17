<template>
  <div>
    <label>
      Filter by Title:
      <input type="text" v-model="title" @input="filterByTitle" />
    </label>
  </div>
</template>

<script>
export default {
  name: "Title-Filter",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    filterByTitle() {
      this.$emit("updateTitle", this.title);
    },
  },
};
</script>
