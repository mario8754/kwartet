<template>
  <div class="playfield">
    <new Date().toLocaleString() />
    <Deck :amount="deck.amount" @draw="draw" />
    <Hand :cards="player.cards" v-if="deck.amount > 50" />
  </div>
</template>

<script>
import Deck from "./Deck.vue";
import Hand from "./Hand.vue";
export default {
  name: "Playfield",
  components: {
    Deck,
    Hand,
  },
  data() {
    return {
      deck: {
        amount: 52,
        cards: [
          {
            type: "Vogel 1",
            value: "A",
          },
          {
            type: "Vogel 1",
            value: "K",
          },
        ],
      },
      player: {
        cards: [
          {
            type: "Vogel 1",
            value: "A",
          },
          {
            type: "Vogel 1",
            value: "K",
          },
        ],
      },
    };
  },
  methods: {
    draw(amount) {
      this.deck.amount = amount;
      this.player.cards.push({
        type: "Vogel 1",
        value: "7",
      });
    },
    reset() {
      this.deck.amount = 52;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.playfield {
  border: 1px solid black;
  height: 550px;
  width: 1100px;
}
</style>
