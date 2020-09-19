<template>
  <div class="hand" @drop="handleDrop" @dragover.prevent @dragenter.prevent>
    <div
      v-for="(card, i) of cards"
      :key="i"
      class="card"
      id="card"
      draggable="true"
      @dragstart="event => registerDrag(event, card)"
    >{{card.type}} - {{card.value}}</div>
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
  methods: {
    registerDrag(event, card) {
      console.log(card);
      event.dataTransfer.setData("drag", event.target.id);
      event.dataTransfer.setData("data", JSON.stringify(card));
    },
    handleDrop(event) {
      event.preventDefault();
      // Hiermee wordt nu gechecked welke drag type ik gebruik.
      if (event.dataTransfer.getData("drag") === "deck") {
        console.log("Drawing card");
        // Als drag type gelijk staat aan deck dan voeren we de drag methode uit.
        this.draw();
      }
    },
    draw() {
      this.$emit("draw");
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