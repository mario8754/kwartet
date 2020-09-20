<template>
  <div class="hand list-group" @drop="handleDrop" @dragover.prevent @dragenter.prevent>
    <draggable>
      <div
        v-for="(card, i) of cards"
        :key="i"
        class="card list-group-item"
        id="card"
        draggable="true"
        @dragstart="event => registerDrag(event, card)"
      >
        <img :src="require(`@/assets/images/${card.value}.png`)" alt="No image" class="img" />
        - {{card.type}}
      </div>
    </draggable>
  </div>
</template>
//invoegen van de draggable 
<script>
import draggable from "vuedraggable";
export default {
  components: {
    draggable,
  },
  props: {
    cards: {
      type: Array,
      required: true,
    },
  },
  //register van de draw
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
  height: 40%;
  width: 100%;
  display: flex;
}

.hand > div {
  width: 100%;
  word-wrap: unset;
}

.card {
  border: 1px solid black;
  height: 200px;
  width: 200px;
  color: red;
  background-color: blue;
  display: inline-block;
}

.img {
  height: 150px;
  width: auto;
  display: flex;
  pointer-events: none;
}
</style>
