<template>
  <!-- <div>
  <div class="kwartet" @drop="handleDrop" @dragover.prevent @dragenter.prevent></div>-->
  <div class="trash" id="trash" @drop="handleDrop" @dragover.prevent @dragenter.prevent>
    <img :src="require(`@/assets/images/${card.value}.png`)" :alt="card.type" class="img" />
    - {{card.type}}
  </div>
</template>

<script>
// Hier logica voor het kaartjes trekken en welke je hebt getrokken
// Hier ook logica voor welke kaarten je door aan het slepen bent.
export default {
  data() {
    return {
      card: {
        type: "Er is nog geen kaart getrashed",
        value: "trash",
      },
    };
  },
  methods: {
    handleDrop(event) {
      event.preventDefault();
      // Hiermee wordt nu gechecked welke drag type ik gebruik.
      if (event.dataTransfer.getData("drag") === "card") {
        console.log(event.dataTransfer.getData("data"));
        this.card = JSON.parse(event.dataTransfer.getData("data"));
        this.handleTrash();
      }

      // Met deze id weet je nu evt welke actie je moet gaan uitvoeren.
    },
    handleTrash() {
      this.$emit("trashed", this.card);
    },
  },
};
</script>

<style scoped>
.trash {
  border: 1px solid black;
  height: 250px;
  width: 150px;
  background: red;
  opacity: 70%;
}
.img {
  height: 150px;
  width: auto;
}
</style>