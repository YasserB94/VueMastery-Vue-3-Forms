<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  id: {
    type: [String, Number],
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
  <label v-show="!labelIsHidden" :for="props.id" class="capitalize">{{
    props.label || props.name
  }}</label>
  <input
    v-bind="$attrs"
    :name="props.name"
    :id="props.id"
    @change="updateValue"
    :checked="modelValue"
    type="checkbox"
  />
</template>

<style scoped></style>
