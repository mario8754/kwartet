<template>
  <!-- <div>
  <div class="kwartet" @drop="handleDrop" @dragover.prevent @dragenter.prevent></div>-->
  <div class="trash" id="trash" @drop="handleDrop" @dragover.prevent @dragenter.prevent>{{card}}</div>
</template>

<script>
// Hier logica voor het kaartjes trekken en welke je hebt getrokken
// Hier ook logica voor welke kaarten je door aan het slepen bent.
export default {
  data() {
    return {
      card: {},
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
}
</style>