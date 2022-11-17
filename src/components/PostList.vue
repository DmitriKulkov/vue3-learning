<template>
  <div>
    <h3>Post List:</h3>
    <transition-group name="post-list">
      <post-item
        v-for="post in posts"
        :key="post.id"
        :post="post"
        @remove="$emit('remove', post)"
      />
    </transition-group>
  </div>
</template>

<script lang="ts">
import { Post } from "@/typings";
import { PropType } from "vue";
import PostItem from "./PostItem.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "post-list",
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

<style lang="scss" scoped>
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter-from,
.post-list-leave-to {
  opacity: 0;
  transform: translateX(130px);
}
.post-list-move {
  transition: transform 0.4s ease;
}
</style>
