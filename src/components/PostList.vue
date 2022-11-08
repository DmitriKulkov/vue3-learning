<template>
  <div v-if="posts.length > 0">
    <h3>Post List:</h3>
    <post-item
      v-for="post in posts"
      :key="post.id"
      :post="post"
      @remove="$emit('remove', post)"
    />
  </div>
  <h2 v-else style="color: red">Posts not fount</h2>
</template>

<script lang="ts">
import { Post } from "@/typings";
import { PropType } from "vue";
import PostItem from "./PostItem.vue";
import { defineComponent } from "vue";

export default defineComponent({
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array as PropType<Post[]>,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped></style>
