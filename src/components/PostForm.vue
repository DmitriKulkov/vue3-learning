<template>
  <form @submit.prevent>
    <h4>Create post</h4>
    <input
      v-model="post.title"
      type="text"
      class="input"
      placeholder="Post title"
    />
    <input
      v-model="post.body"
      type="text"
      class="input"
      placeholder="Post description"
    />
    <button class="btn" @click="createPost">Create</button>
  </form>
</template>

<script lang="ts">
export default {
  data() {
    return {
      post: { id: 0, title: "", body: "" },
    };
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        id: 0,
        title: "",
        body: "",
      };
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./common/common";

%form-element {
  padding: 10px 15px;
  margin-top: 15px;
  @include border(1px);
}

.input {
  @extend %form-element;
  width: 100%;
}

.form {
  display: flex;
  flex-direction: column;
}

.btn {
  @extend %form-element;
  align-self: flex-end;
  background: none;
  color: $main-color;
}
</style>
