<template>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  <PickASign v-if="isPickASignState" @submitConfig="runAGame" />
  <GameComp v-if="isGameCompState" :configurations="configurations"/>
  <Game v-if="isGameState" :configurations="configurations" @submitResult="results" />
  <Score v-if="isScoreState" :trs="trs"  @startNew="startNewGame"/>
</template>

<script>
import PickASign from "./components/PickASign.vue";
import Game from "./components/Game.vue";
import GameComp from "./components/GameComp.vue";
import Score from "./components/Score.vue";

export default {
  name: "App",
  components: {
    PickASign,
    Game,
    GameComp,
    Score,
  },
  computed: {
    isPickASignState() {
      return this.gameState == "pickasign";
    },
    isGameState() {
      return this.gameState == "gamestate";
    },
    isGameCompState() {
      return this.gameState == "gameStateComp";
    },
    isScoreState() {
      return this.gameState == "score";
    },
  },
  data() {
    return {
      gameState: "pickasign",
      configurations: {
        pickedSign: "",
        player: "",
        opponentSign: "",
      },
      trs: {
        matrix: [
          [" ", " ", " "],
          [" ", " ", " "],
          [" ", " ", " "],
        ],
        counters: [[0, 0], [0, 0], [0, 0], 0],
        opponent: "",
        winner: "",
      },
      newGame: false,
    };
  },
  methods: {
    runAGame(config) {
      var self = this;
      self.configurations = config;
      console.log(self.configurations);
      if (self.configurations.player == "friend") this.gameState = "gamestate";
      else {
        this.trs.opponent = self.configurations.player;
        console.log(this.trs.opponent);
        this.gameState = "gameStateComp";
      }
    },
    results(trs) {
      var self = this;
      self.trs = trs;
      console.log(self.trs);
      this.gameState = "score";
    },
    startNewGame() {
      this.gameState="pickasign";
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

/* .inner {
  background-color: burlywood;
} */
</style>
