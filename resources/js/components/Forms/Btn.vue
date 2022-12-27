<template>
  <div>
    <button
      :class="'btn btn-' + buttons[btnType]"
      @click="btnAction"
    >{{btnTxt}}</button>
  </div>
</template>

<script>
export default {
  props: {
    btnType: String,
    btnTxt: String,
    btnAction: Function,
  },
  data() {
    return {
      buttons: {
        save: "success",
        remove: "danger",
        edit: "warning",
        cancel: "danger",
      },
    };
  },
};
</script>

<style>
</style>
