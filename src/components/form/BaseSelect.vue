<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  options: {
    type: Array,
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
    type: [String, Number],
  },
});
const emit = defineEmits(["update:modelValue"]);
const updateValue = (e) => {
  emit("update:modelValue", e.target.value);
};
</script>

<template>
  <label v-show="!labelIsHidden" :for="props.name" class="capitalize">{{
    props.label || props.name
  }}</label>
  <select
    v-bind="$attrs"
    :name="props.name"
    @change="updateValue"
    :value="modelValue"

  >
    <option value="" disabled selected hidden>{{ props.label||props.name }}...</option>
    <option
      v-for="(option, index) in props.options"
      :key="`${index}${option}`"
      :selected="option === modelValue"
    >
      {{ option }}
    </option>
  </select>
</template>

<style scoped></style>
