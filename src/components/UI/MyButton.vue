<template>
  <button class="my_btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: "my-button",
};
</script>

<style lang="scss" scoped>
@import "@/components/common/form-element";
.my_btn {
  @extend %form-element;
  background: none;
  color: $main-color;
  height: 40px;
  width: 120px;
}
</style>
