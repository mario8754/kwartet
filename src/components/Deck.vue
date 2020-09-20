<template>
  <div class="deck" id="deck" draggable="true" @dragstart="registerDrag">{{amount}}</div>
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
    registerDrag(event) {
      event.dataTransfer.setData("drag", event.target.id);
    },
  },
};
</script>

<style scoped>
.deck {
  border: 1px solid black;
  height: 250px;
  width: 150px;
  background: green;
  margin-bottom: 2rem;
  margin-left: 2rem;
}
</style>