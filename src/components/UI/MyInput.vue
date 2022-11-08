<template>
  <input :value="modelValue" class="input" type="text" @input="updateInput" />
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "my-input",
  props: {
    modelValue: [String, Number],
  },
  methods: {
    updateInput(event: Event): void {
      this.$emit("update:modelValue", (event.target as HTMLInputElement).value);
    },
  },
});
</script>

<style lang="scss" scoped>
@import "@/components/common/form-element";
.input {
  @extend %form-element;
  width: 100%;
}
</style>
