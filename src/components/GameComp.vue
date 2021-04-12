<template>
  <div class="inner">
    <div>
      <p>Player: {{ configurations.pickedSign }}</p>
      <p>Computer: {{ configurations.opponentSign }}</p>
    </div>
    <div>
      <table>
        <tr v-for="(line, id) in trs.matrix" :key="line.id">
          <td
            v-for="(cell, id1) in line"
            :key="cell.id1"
            @click="setSign(id, id1)"
          >
            {{ cell }}
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  name: "GameComp",
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
        counters: [[0, 0], [0, 0], [0, 0], 0],
        winner: "",
        field: {
          row: "",
          column: "",
        },
      },
      firstStep: false,
    };
  },
  methods: {
    setSign(x, y) {
      if (this.trs.matrix[x][y] == " ") {
        this.trs.matrix[x][y]==this.configurations.pickedSign
    
        
      }
      // oponent(){
           
      // }
    }
  },
  mounted() {
    for (let tr in this.trs.matrix) {
      tr = new this.field(tr);
    }
  },
}
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
</style>
