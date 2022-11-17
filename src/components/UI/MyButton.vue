<template>
  <button class="my_btn">
    <slot></slot>
  </button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "my-button",
});
</script>

<style lang="scss" scoped>
@import "@/components/common/form-element";
.my_btn {
  @extend %form-element;
  background: none;
  color: $primary-color;
  height: 40px;
  width: 120px;
}
</style>
