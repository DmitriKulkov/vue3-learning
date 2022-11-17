<template>
  <select :value="modelValue" @change="changeOption" class="select">
    <option disabled value="">Options:</option>
    <option v-for="option in options" :key="option.value" :value="option.value">
      {{ option.name }}
    </option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { PropType } from "vue";

export default defineComponent({
  name: "my-select",
  props: {
    modelValue: {
      type: String,
    },
    options: {
      type: Array as PropType<Array<{ value: string; name: string }>>,
      default: () => [],
    },
  },
  methods: {
    changeOption(event: Event) {
      this.$emit(
        "update:modelValue",
        (event.target as HTMLSelectElement).value
      );
    },
  },
});
</script>

<style lang="scss" scoped>
@import "@/components/common/form-element";
.select {
  @extend %form-element;
}
</style>
