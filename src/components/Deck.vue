<template>
  <div class="deck" @click="draw">{{amount}}</div>
</template>

<script>
export default {
  props: {
    amount: {
      type: Number,
      required: true,
    },
  },
  methods: {
    draw() {
      this.$emit("draw", this.amount - 1);
    },
  },
};
</script>

<style scoped>
.deck {
  border: 1px solid black;
  height: 250px;
  width: 150px;
}
</style>