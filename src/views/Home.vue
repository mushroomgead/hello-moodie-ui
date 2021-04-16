<template>
  <h1>Overview {{ title }}</h1>
  <div class="container-body"></div>
  <span v-for="item in items" :key="item.id" :load="log(item)">
    {{ item.username }}
  </span>
  <button v-on:click="handleOnAdd">add mood today</button>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  data() {
    return {
      items: [],
    };
  },
  async created() {
    let result = await axios.get("http://localhost:4000/user");
    this.items = result.data;
  },
  methods: {
    log(item) {
      console.log("item: ", item);
    },
    handleOnAdd() {
      console.log("click item");

      this.$router.push("about");
    },
  },
};
</script>

<style scoped></style>
