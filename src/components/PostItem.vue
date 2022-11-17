<template>
  <div class="post">
    <div class="post__description">
      <div><strong>Title: </strong>{{ post.title }}</div>
      <div><strong>Descrption: </strong>{{ post.body }}</div>
    </div>
    <my-button @click="$emit('remove', post)">Delete</my-button>
  </div>
</template>

<script lang="ts">
import { PropType } from "vue";
import { Post } from "@/typings";
import { defineComponent } from "vue";

export default defineComponent({
  name: "post-item",
  props: {
    post: {
      type: Object as PropType<Post>,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped>
@import "./common/border";

.post {
  padding: 15px;
  margin-top: 15px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  @include border(3px);
}

.post__description {
  display: flex;
  flex-direction: column;
  gap: 5px;
}
</style>
