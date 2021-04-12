<template>
<div class="inner">
  <img
    alt="Vue logo"
    src="../assets/kisspng-tic-tac-toe-oxo-cross-round-chokdi-mindu-tic-tac-chess-game-5ade7fdabdd870.4782875515245311627776.png"
  />
  <div>
    <h1>Welcome to the Tic Tac Toe Game!</h1>
  </div>
  <div id="choose">
    <div class="card">
      <p>Choose your sign</p>

      <input type="radio" name="sign" id="0" value="X" v-model="configurations.pickedSign" />
      <label for="X">Start game with sign X</label><br />

      <input type="radio" name="sign" id="1" value="O" v-model="configurations.pickedSign" key=""/>
      <label for="O">Start game with sign O</label>
    </div>

    <div class="card">
      <p>Choose an opponent</p>

      <input type="radio" name="opponent" id="friend" value="friend" v-model="configurations.player" />
      <label for="friend">Play with a friend</label><br />

      <input type="radio" name="opponent" id="comp" value="comp" v-model="configurations.player" />
      <label for="comp">Play with a computer</label>
    </div>
  </div>
  <div class="card">
    <p>
      You choose to play with {{  configurations.pickedSign != "" ? configurations.pickedSign : "(please choose your sign)" }}
      sign with a {{ configurations.player != "" ? configurations.player : "(Please choose your opponent)" }}
    </p>
  </div>
</div>
  <input type="submit" value="Start A Game" @click="submitConfig" />
</template>

<script>
export default {
  name: "PickASign",
  data() {
    return {
      configurations: {
        pickedSign: "",
        player: "",
        opponentSign: "",
      },
    };
  },
  methods: {
    submitConfig() {
      if (
        (this.configurations.pickedSign != "") &
        (this.configurations.player != "")
      ) {
        if (this.configurations.pickedSign == "X") this.configurations.opponentSign = "O"
        else this.configurations.opponentSign = "X";
        console.log(this.configurations);
        this.$emit("submitConfig", this.configurations);
      }
    },
  },
};
</script>

<style>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  border: 2pt double #ff9800;
  width: 30%;
  margin-left: 35%;
  margin-top: 20pt;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  width: 31%;
  margin-left: 34.5%;
}

h1 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

.card p {
  text-decoration: black underline;
  font-weight: bold;
}

input[type="submit"] {
  box-shadow: 0 4px 8px 0 rgb(231, 181, 87);
  transition: 0.3s;
  border: 2pt double rgb(231, 181, 87);
  width: 16%;
  padding: 12pt 20pt 12pt 20pt;
  margin-top: 0.5%;
  background-color: #ff9800;
}

input[type="submit"]:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  width: 16%;
}

img {
  width: 20%;
}
</style>
