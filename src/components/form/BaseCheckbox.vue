<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  label: {
    type: String,
  },
  labelIsHidden: {
    type: Boolean,
    default: false,
  },
  modelValue: {
    type: Boolean,
    default: false,
  },
});
const emit = defineEmits(["update:modelValue"]);
const updateValue = (e) => {
  emit("update:modelValue", e.target.checked);
};
</script>

<template>
  <label v-show="!labelIsHidden" :for="props.name" class="capitalize">{{
    props.label || props.name
  }}</label>
  <input
    v-bind="$attrs"
    :name="props.name"
    @change="updateValue"
    :checked="modelValue"
    type="checkbox"
  />
</template>

<style scoped></style>
