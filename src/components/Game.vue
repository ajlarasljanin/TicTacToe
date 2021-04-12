<template>
  <div class="inner">
    <div class="card">
      <h1>Tic Tac Toe Game - GOOD LUCK</h1>
    </div>
    <div class="card">
      <p>
        <strong>Player 1: {{ configurations.pickedSign }}</strong>
      </p>
      <p>
        <strong>Player 2: {{ configurations.opponentSign }}</strong>
      </p>
    </div>
    <div>
      <table>
        <tr v-for="(line, id) in trs.matrix" :key="line.id">
          <td v-for="(cell, id1) in line" :key="cell.id1" @click="setSign(id, id1)">
            {{ cell }}
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  name: "Game",
  props: ["configurations"],
  data() {
    return {
      title: "Game",
      numberOfClicks: 0,
      trs: {
        matrix: [
          [" ", " ", " "],
          [" ", " ", " "],
          [" ", " ", " "],
        ],
        counters: [0, 0, 0, 0, 0],
        winner: "",
      },
    };
  },
  methods: {
    setSign(x, y) {
      if (this.trs.matrix[x][y] == " ") {
        var currentInput = "";
        if (this.numberOfClicks % 2 == 0)
          currentInput = this.configurations.pickedSign;
        else currentInput = this.configurations.opponentSign;
        this.trs.matrix[x][y] = currentInput;
        this.numberOfClicks++;

        let rowNew = 0;
        let columnNew = 0;
        let diagonalNew = 0;
        let subdiagonalNew = 0;
        for (var i = 0; i < 3; i++) {
          if (this.trs.matrix[x][i] == currentInput) rowNew++;
          if (this.trs.matrix[i][y] == currentInput) columnNew++;
          if (this.trs.matrix[i][i] == currentInput) diagonalNew++;
          if (this.trs.matrix[2 - i][i] == currentInput) subdiagonalNew++;
        }

        if (
          rowNew == 3 ||
          columnNew == 3 ||
          diagonalNew == 3 ||
          subdiagonalNew == 3
        ) {
          if (rowNew == 3) {
            // this.trs.counters[0][0] = rowNew;
            this.trs.counters[0] = x;
          }
          if (columnNew == 3) {
            // this.trs.counters[1][0] = columnNew;
            this.trs.counters[1] = y;
          }
          if (diagonalNew == 3) this.trs.counters[2] = 1;
          if (subdiagonalNew == 3) this.trs.counters[3] = 1;
          this.trs.winner = currentInput;
          console.log("Player " + currentInput + " has won!");
          console.log(this.trs.counters);
          this.$emit("submitResult", this.trs);
        }

        if (this.numberOfClicks == 9 && this.trs.counters[0]==0
         && this.trs.counters[1]==0  && this.trs.counters[2]==0
          && this.trs.counters[3]==0) {
          this.trs.winner = "";
          this.trs.counters[4] = this.numberOfClicks;
          this.$emit("submitResult", this.trs);
        }
      }
    },
  },
  mounted() {
    // console.log(this.configurations);
  },
};
</script>
<style>
table {
  border-collapse: collapse;
  margin-left: 43%;
  margin-top: 10%;
}
table td {
  border: 5px solid black;
  height: 80pt;
  width: 80pt;
  border-color: #ff9800;
}
table tr:first-child td {
  border-top: 0;
  border-color: #ff9800;
}
table tr td:first-child {
  border-left: 0;
  border-color: #ff9800;
}
table tr:last-child td {
  border-bottom: 0;
  border-color: #ff9800;
}
table tr td:last-child {
  border-right: 0;
  border-color: #ff9800;
}

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
</style>
