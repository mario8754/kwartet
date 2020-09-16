<template>
  <div class="playfield">
    <Deck :amount="deck.amount" @draw="draw" />
    <Hand :cards="player.cards" v-if="deck.amount > 12" />
  </div>
</template>

<script>
// Hier logica over het spel in het algemeen
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
        amount: 12,
        // Ik ben nog bij me ma en lucca slaapt dus ik kan niet echt praten
        // Ik hoor je wel
        // Dat klopt wel over het algmeen css is meestal een bijproduct

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
          {
            type: "Vogel 2",
            value: "K",
          },
          {
            type: "Vogel 2",
            value: "K",
          },
        ],
      },
    };
  },
  // Mounted wordt aangeroepen wanneer de component zichtbaar is voor de gebruiker.
  mounted() {
    // Wanneer de pagina beschikbaar is wil je de deck aanmaken.
    this.startGame();
  },
  methods: {
    startGame() {
      // Hier zou je je logica van het opstellen van een deck maken.
      // Ja precies dus de volgorde in deze code zou een beetje zijn
      this.generateDeck();
      this.shuffleDeck();
      this.draw();
      this.draw();
      this.draw();
      this.draw();

      // zoiets.
    },
    generateDeck() {
      // Hier logica om een matrix op te stellen en die dan samen te voegen in 1 array om een deck te krijgen.
    },
    shuffleDeck() {
      // Hier om de deck te random sorteren.
    },
    draw(amount) {
      this.deck.amount = amount;
      this.player.cards.push({
        type: "Vogel 1",
        value: "7",
      });
    },
    reset() {
      this.deck.amount = 12;
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
