<template>
  <div class="post">
    <div>
      <div><strong>Title: </strong>{{ post.title }}</div>
      <div><strong>Descrption: </strong>{{ post.body }}</div>
    </div>
  </div>
</template>

<script lang="ts">
import { PropType } from "vue";
import { Post } from "@/typings";

export default {
  props: {
    post: {
      type: Object as PropType<Post>,
      required: true,
    },
  },
};
</script>

<style lang="scss" scoped>
@import "./common/common";

.post {
  padding: 15px;
  margin-top: 15px;
  @include border(2px);
}
</style>
