<template>
  <div class="create">
    <h1></h1>
    <label for="mood">please select your mood</label>
    <select v-model="status">
      <option disabled value="">Please select one</option>
      <option>happy</option>
      <option>sad</option>
      <option>soso</option>
      <option>excited</option>
    </select>
    <label for="note">note</label>
    <textarea
      id="note"
      name="note"
      rows="3"
      cols="50"
      v-model="note"
    ></textarea>
    <div>
      <button v-on:click="handleOnClick">save</button>
      <button v-on:click="handleOnBack">back</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      status: "happy",
      note: "",
      id: "e99b1a94-a3fa-421f-95e8-a270202fa62f",
    };
  },
  methods: {
    async handleOnClick() {
      const data = {
        status: this.status,
        note: this.note,
        id: this.id,
      };
      let result = await axios.post("http://localhost:4000/mood/create", data);

      if (result.data === "created") {
        this.$router.push("/");
      }
    },
    handleOnBack() {
      this.$router.back();
    },
  },
};
</script>

<style scoped>
.create {
  display: flex;
  flex-direction: column;
}
</style>
