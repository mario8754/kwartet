<template>
  <div class="playfield">
    <button @click="reset">reset</button>
    <button @click="checkKwartet">kwartet</button>
    <button @click="instructie">instructie</button>
    <div class="flex">
      <Deck :amount="deck.cards.length" />
      <Trash @trashed="trashedCardOutOfHand" />
    </div>
    <Hand :cards="player.cards" @draw="drawTopCardInDeck" />
  </div>
</template>

<script>
// Hier logica over het spel in het algemeen. Hier worden de klasse geimporteerd.
import Deck from "./Deck.vue";
import Hand from "./Hand.vue";
import Trash from "./Trash.vue";

export default {
  name: "Playfield",
  components: {
    Deck,
    Hand,
    Trash,
  },
  data() {
    return {
      deck: {
        cards: [],
      },
      player: {
        cards: [],
      },
    };
  },
  // Mounted wordt aangeroepen wanneer de component zichtbaar is voor de gebruiker.
  mounted() {
    // Wanneer de pagina beschikbaar is wordt de deck aangemaakt.
    this.startGame();
  },
  methods: {
    startGame() {
      // window.alert("creating cards");
      // Hier zou je je logica van het opstellen van een deck maken.
      // Ja precies dus de volgorde in deze code zou een beetje zijn
      this.generateDeck();
      this.shuffleDeck();
      this.drawTopCardInDeck();
      this.drawTopCardInDeck();
      this.drawTopCardInDeck();
      this.drawTopCardInDeck();

      // zoiets.
    },
    // Hier logica om een matrix op te stellen en die dan samen te voegen in 1 array om een deck te krijgen.
    generateDeck() {
      const types = ["Vogel-1", "Vogel-2", "Vogel-3", "Vogel-4"];
      const values = ["A", "B", "C", "D"];

      // Loop door alle types
      const deck = types.map((type) => {
        // Loop door alle values
        const row = values.map((value) => {
          return {
            type: type,
            value: value,
          };
        });
        return row;
      });
      //Voegt Array samen
      this.deck.cards = deck.flat();
    },
    shuffleDeck() {
      // Hier om de deck te random sorteren.
      window.alert("Shuffling DecK");

      this.deck.cards.sort(() => Math.random() - 0.5);
    },
    drawTopCardInDeck() {
      if (this.deck.cards.length === 0) {
        window.alert("NO CARDS je kan de Game resetten");
        return;
      }

      if (this.player.cards.length === 4) {
        window.alert("Maximaal maar 4 kaarten in hand");
        return;
      }
      // Sla bovenste kaart op uit de deck
      const topCard = this.deck.cards[0];
      // Haal bovenste kaart uit deck
      this.deck.cards.shift();
      // Zet de opgeslagen kaart in mijn hand
      this.drawCard(topCard);
    },
    drawCard(card) {
      this.player.cards = this.player.cards.concat(card);
    },
    //reloaden van het spel bij een reset
    reset() {
      window.location.reload();
    },
    //instructie voor het spel
    instructie() {
      window.alert(
        "Het is de bedoeling dat je vogels 4 van de zelfde vogels in je handen hebt. Je mag 1 keer wegslepen om een andere te pakken. A:s je 4 van dezelfde kaarten hebt, kun je op kwartet klikken. Bij kwartet kun je een nieuw spel starten door op reset te klikken."
      );
    },
    //Check of de speler kwartet heeft
    checkKwartet() {
      const valueToCheck = this.player.cards[0].value;
      const hasKwartet = this.player.cards.every(
        (card) => card.value === valueToCheck
      );
      if (hasKwartet && this.player.cards.length === 4) {
        window.alert("KWARTET!");
        window.location.reload();
      } else {
        window.alert("Je hebt geen kwartet!");
      }
    },
    // methode voor het wegleggen van de kaarten en ook check dat de speler niet minder dan 4 kaarten heeft.
    trashedCardOutOfHand(trashedCard) {
      if (this.player.cards.length < 4) {
        window.alert("U moet eerst een kaart pakken");
        return;
      }
      this.player.cards = this.player.cards.filter(
        (card) =>
          !(card.type === trashedCard.type && card.value === trashedCard.value)
      );
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.playfield {
  height: 95vh;
  width: 100%;
}

.flex {
  display: flex;
  justify-content: space-between;
}
.button {
  margin: 1px;
}
</style>
