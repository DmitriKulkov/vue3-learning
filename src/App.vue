<template>
  <div class="app">
    <h1>Posts page</h1>
    <my-button @click="showDialog" style="margin: 15px 0"
      >Create post</my-button
    >
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>
    <post-list :posts="posts" @remove="removePost" />
  </div>
</template>

<script lang="ts">
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import { defineComponent } from "vue";
import { Post } from "@/typings";
export default defineComponent({
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [
        { id: 1, title: "JS post", body: "Post description" },
        { id: 2, title: "JS post 2", body: "Post description 2" },
        { id: 3, title: "JS post 3", body: "Post description 3" },
        { id: 4, title: "JS post 4", body: "Post description 4" },
      ] as Post[],
      title: "",
      body: "",
      dialogVisible: false,
    };
  },
  methods: {
    createPost(post: Post): void {
      this.posts.push(post);
    },
    removePost(post: Post): void {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
  },
});
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>
