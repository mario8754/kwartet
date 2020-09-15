<template>
  <div class="hand">
    <div class="card" v-for="(card, i) in cards" :key="i">{{card.type}} - {{card.value}}</div>
  </div>
</template>

<script>
export default {
  props: {
    cards: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.hand {
  border: 1px solid black;
  height: 250px;
  width: 1100px;
  display: flex;
}

.card {
  border: 1px solid black;
  height: 250px;
  width: 175px;
}
</style>