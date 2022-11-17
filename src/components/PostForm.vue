<template>
  <form @submit.prevent class="form">
    <h4>Create post</h4>
    <my-input v-model="post.title" type="text" placeholder="Post title" />
    <my-input v-model="post.body" type="text" placeholder="Post description" />
    <my-button class="btn" style="align-self: flex-end" @click="createPost"
      >Create</my-button
    >
  </form>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "post-form",
  data: () => {
    return {
      post: { id: 0, title: "", body: "" },
    };
  },
  methods: {
    createPost(): void {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        id: 0,
        title: "",
        body: "",
      };
    },
  },
});
</script>

<style lang="scss" scoped>
@import "./common/form-element";

.form {
  display: flex;
  flex-direction: column;
  gap: 15px;
}
</style>
