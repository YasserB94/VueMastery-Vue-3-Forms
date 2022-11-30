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
  error: {
    type: String,
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
  <label v-show="!labelIsHidden" :for="props.id" class="capitalize">{{
    props.label || props.name
  }}</label>
  <input
    v-bind="$attrs"
    :name="props.name"
    :id="props.id"
    :type="props.type"
    :class="[{ 'placeholder:capitalize': !props.placeholder }]"
    :placeholder="props.placeholder || `${props.name}...`"
    @input="updateValue"
    :aria-describedby="`${props.id}-error`"
  />
  <p :id="`${props.id}-error`" v-if="props.error" class="text-xs text-red-800">
    {{ props.error }}
  </p>
</template>

<style scoped></style>
