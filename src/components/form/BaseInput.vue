<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    default: "text",
  },
  placeholder: {
    type: String,
  },
  label: {
    type: String,
  },
  labelIsHidden: {
    type: Boolean,
    default: false,
  },
  stylesInput: {
    type: [Array, String, Object],
  },
  stylesLabel: {
    type: [Array, String, Object],
  },
  modelValue: {
    type: [String, Number],
  },
});
const emit = defineEmits(["update:modelValue"]);
const updateValue = (e) => {
  emit("update:modelValue", e.target.value);
};
</script>
<template>
  <label
    v-show="!props.labelIsHidden"
    :for="props.name"
    :class="stylesLabel"
    class="capitalize"
    >{{ props.label || props.name }}</label
  >
  <input
      v-bind="$attrs"
    :name="props.name"
    :type="props.type"
    :class="[
      { 'placeholder:capitalize': !props.placeholder },
      props.stylesInput,
    ]"
    :placeholder="props.placeholder || `${props.name}...`"
    @input="updateValue"
  />
</template>

<style scoped></style>
