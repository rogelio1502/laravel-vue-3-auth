<template>
  <div
    :class="'alert alert-' + alerts[type]  + ' alert-dismissible fade show'"
    role="alert"
    v-show="true"
  >
    {{alertTxt}}
    <button
      type="button"
      class="btn-close"
      data-bs-dismiss="alert"
      aria-label="Close"
    ></button>
  </div>
</template>

<script>
export default {
  props: {
    type: String,
    alertTxt: String,
  },
  data() {
    return {
      alerts: {
        success: "success",
        warning: "warning",
      },
    };
  },
};
</script>

<style>
</style>
