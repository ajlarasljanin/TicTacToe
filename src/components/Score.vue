<template>
<div class="inner">
  <div>
    <h1>Result</h1>
    <h2>{{ result }}</h2>
  </div>
  <div>
    <table>
      <tr v-for="line in trs.matrix" :key="line.id" v-bind:style="{row==line ? color:aquamarine;  background-color: cadetblue : ' '}" >
        <td v-for="cell in line" :key="cell.id1">{{ cell }}</td>
      </tr>
    </table>
  </div>
  <div>
    <h4>Play new game</h4>
    <button @click="startNew">Start!</button>
  </div>
</div>
</template>
<script>
export default {
  title: "Score",
  props: ["trs"],
  data() {
    return {
      result: "",
      row: {
        type: Number,
        default: 10., 
      },
      column: {
        type: Number,
        default: 10,
      },
      diagonal: {
        type: Number,
        default: 10,
        
      },
      subdiagonal: {
        type: Number,
        default: 10,
      }
    };
  },
  methods: {
    startNew() {
      this.$emit("startNew");
    },

  },
  mounted() {
    if (this.trs.winner != ""){
      this.result = `Player ${this.trs.winner} has won!`;
      if (this.trs.counters[0]==1) this.row=this.trs.counters[0]
      }
    else this.result = `No winner this time!`;
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

.winn {
  color:aquamarine;
  background-color: cadetblue;
}
</style>
