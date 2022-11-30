<script setup>
import BaseRadio from "./BaseRadio.vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  options: {
    type: Array,
    required: true,
  },
  vertical:{
    type:Boolean,
    default:false
  },
  modelValue: {
    type: [String, Number],
    required: true,
  },
});
const emit = defineEmits(["update:modelValue"]);
const updateValue = (e) => {
  emit("update:modelValue", e);
};
</script>

<template>
  <component v-for="option in options" :key="option.value" :is="props.vertical?'div':'span'" :class="vertical?'mt-2':'mr-2'">
    <BaseRadio
      :label="option.label"
      :value="option.value"
      :modelValue="modelValue"
      :name="name"
      @update:modelValue="updateValue"
    />
  </component>
</template>

<style scoped></style>
