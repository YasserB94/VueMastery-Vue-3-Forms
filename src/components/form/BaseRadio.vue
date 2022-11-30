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
  value: {
    type: [String, Number],
    required: true,
  },
  labelIsHidden: {
    type: Boolean,
    default: false,
  },
  modelValue: {
    type: [String, Number],
  },
});
const emit = defineEmits(["update:modelValue"]);
const updateValue = () => {
  emit("update:modelValue", props.value);
};
</script>

<template>
  <input
    v-bind="$attrs"
    :value="props.value"
    :id="props.id"
    :name="`${props.name}`"
    type="radio"
    @change="updateValue"
  />
  <label
    v-show="!labelIsHidden"
    :for="props.id"
    class="capitalize"
    >{{ props.label || props.name }}</label
  >
</template>

<style scoped></style>
