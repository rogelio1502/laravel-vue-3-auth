<template>
  <div class="mb-3">
    <label
      :for="inputId"
      class="form-label"
    >{{inputLabel}}</label>
    <textarea
      class="form-control"
      :id="inputId"
      :value="modelValue"
      @input="$emit('update:modelValue',$event.target.value)"
    ></textarea>
  </div>
</template>

<script>
export default {
  props: {
    inputId: String,
    inputLabel: String,
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
