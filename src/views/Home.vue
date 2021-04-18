<template>
  <ul>
    <li v-for="item in items" :key="item.id">
      {{ item.created_date }} | {{ item.status }}
    </li>
  </ul>
  <button v-on:click="handleOnAdd">add mood</button>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      items: [],
    };
  },
  async created() {
    let result = await axios.get("http://localhost:4000/mood/all");
    this.items = result.data;
  },
  methods: {
    handleOnAdd() {
      this.$router.push("create");
    },
  },
};
</script>

<style scoped></style>
