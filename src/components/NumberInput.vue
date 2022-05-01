<template>
  <input :value="modelValue" @input="emitValue" type="number" />
</template>

<script>
export default {
  name: "NumberInput",
  model: {
    prop: "modelValue",
  },
  props: {
    value: {
      type: Number,
      default: 0,
    },
    modelValue: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    emitValue({ target: { value } }) {
      if (value === "") {
        value === 0;
      }
      this.$emit("input", Number(value));
    },
  },
};
</script>
