<template>
  <div class="app">
    <post-form @create="createPost" />
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
    };
  },
  methods: {
    createPost(post: Post): void {
      this.posts.push(post);
    },
    removePost(post: Post): void {
      this.posts = this.posts.filter((p) => p.id !== post.id);
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
