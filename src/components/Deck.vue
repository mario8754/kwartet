<template>
  <div>
    <div class="kwartet" @drop="handleDrop" @dragover.prevent @dragenter.prevent></div>
    <div class="deck" id="deck" draggable="true" @dragstart="registerDrag">{{amount}}</div>
    <div class="hand" @drop="handleDrop" @dragover.prevent @dragenter.prevent>
      <div
        class="card"
        id="card"
        draggable="true"
        @dragstart="registerDrag($event, {type:'bird-one',value:'A'})"
      ></div>
    </div>
  </div>
</template>

<script>
// Hier logica voor het kaartjes trekken en welke je hebt getrokken
// Hier ook logica voor welke kaarten je door aan het slepen bent.
export default {
  props: {
    amount: {
      type: Number,
      required: true,
    },
  },
  methods: {
    registerDrag(event, card) {
      console.log(card);
      // Hiermee registreer je nu de type drag dat je uitvoert.
      event.dataTransfer.setData("drag", event.target.id);
      if (event.target.id === "card") {
        event.dataTransfer.setData("data", JSON.stringify(card));
        console.log(event.dataTransfer.getData("data"));
      }
      // Nu bepaal je de data als die nodig is.

      // console.log(event.dataTransfer.getData("draw"));
      // Registreer welke item je dragt op dat moment.
    },
    handleDrop(event) {
      event.preventDefault();
      // Hiermee wordt nu gechecked welke drag type ik gebruik.
      if (event.dataTransfer.getData("drag") === "deck") {
        console.log("Drawing card");
        // Als drag type gelijk staat aan deck dan voeren we de drag methode uit.
        this.draw();
      } else {
        // Als de drag type niet een deck is gaan we dervanut dat het een card drag is.
        // Als dat zo is willen we weten welke kaart we trekken
        // Om zo straks onze validatie  op uit te voeren.
        console.log(event.dataTransfer.getData("data"));
      }
      // Met deze id weet je nu evt welke actie je moet gaan uitvoeren.
    },
    draw() {
      this.$emit("draw", this.amount - 1);
    },
  },
};
</script>

<style scoped>
.deck,
.card {
  border: 1px solid black;
  height: 250px;
  width: 150px;
}
.hand,
.kwartet {
  border: 1px solid black;
  height: 250px;
  width: 1100px;
}
</style>