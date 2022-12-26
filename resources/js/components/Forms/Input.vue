<template>
  <div class="mb-3">
    <label
      :for="inputId"
      class="form-label"
    >{{inputLabel}}</label>
    <input
      :type="inputType"
      class="form-control"
      :id="inputId"
      :value="modelValue"
      @input="$emit('update:modelValue',$event.target.value)"
    >
  </div>
</template>

<script>
export default {
  props: {
    inputId: String,
    inputLabel: String,
    inputType: String,
    modelValue: String,
  },
  emits: ["update:modelValue"],
  data() {
    return {};
  },
};
</script>

<style>
</style>
