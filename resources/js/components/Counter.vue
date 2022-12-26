<template>
  <div>
    <p>{{number}}</p>
    <button @click="addOne">+</button>
    <button
      :disabled="sustractEnabled == false"
      @click="sustractOne"
    >-</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      number: 0,
      sustractEnabled: this.number > 0 ? true : false,
    };
  },

  methods: {
    addOne() {
      this.number++;
    },
    sustractOne() {
      this.number--;
    },
  },
  watch: {
    number(newValue, oldValue) {
      if (newValue < 1) {
        this.number = 0;
        this.sustractEnabled = false;
      } else {
        this.sustractEnabled = true;
      }
    },
  },
};
</script>

<style>
</style>
