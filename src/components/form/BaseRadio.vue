<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  label: {
    type: String,
  },
  value:{
    type:[String,Number],
    required:true
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
  <label v-show="!labelIsHidden" :for="`radio-${props.name}`" class="capitalize">{{
    props.label || props.name
  }}</label>
  <input
      v-bind="$attrs" :value="props.value" :name="`radio-${props.name}`"  type="radio" @change="updateValue" />
</template>

<style scoped></style>
