<template>
  <div>
    <h3>Post List:</h3>
    <post-item v-for="post in posts" :key="post.id" :post="post" />
  </div>
</template>

<script lang="ts">
import { Post } from "@/typings";
import { PropType } from "vue";
import PostItem from "./PostItem.vue";
export default {
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array as PropType<Post[]>,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped></style>
