<template>
  <div id="app" class="full">
    <header>
      <div class="container">
        <img alt="logo" src="./assets/logo.png">
        <div>
          <h1>Data visualization Football WorldCup 2018</h1>
          <div>
              <b-button pill variant="outline-secondary" class="button" v-on:click="switchView('intro')">Home</b-button>
              <b-button target="_blank" pill variant="outline-secondary" class="button"><a target="_blank" href="https://public.tableau.com/profile/hoyet.lorenz#!/vizhome/DatavizWorldCup2018/DatavizWorldCup2018">Public Tableau</a></b-button>
              <b-button pill variant="outline-secondary" class="button" v-on:click="switchView('players')">Online Visualization</b-button>
          </div>
        </div>
      </div>
    </header>
    <Intro
      v-if="displayViz === 'intro'"
    />
    <Players
      v-if="displayViz === 'players'"
      :players="players"
    />
  </div>
</template>

<script>
import * as d3 from "d3";
import Intro from "./components/Intro"
import Players from "./components/Players"

export default {
  name: 'app',
  components: {
    Players,
    Intro
  },
  mounted() {
    this.fetchData();
  },
  data: function() {
    return {
      displayViz: 'intro',
      players: []
    };
  },
  methods: {
    async fetchData() {
      let DataPlayers = await d3.csv(
        "./datasets/TotalDataPlayers.csv"
      );

      // d3.csv("./datasets/TotalDataPlayers.csv").then(function(data) {
      //   console.log(data[0]);
      // });

      this.players = DataPlayers;
    },
    switchView(e) {
      this.displayViz = e;
    },
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
.full{
  display: block;
  position: relative;
  height: 100vh;
}
.full::after{
  content: "";
  opacity: 0.3;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  position: absolute;
  z-index: -1;  
  background: url("./assets/back.jpg");
}
h1{
  margin-bottom: 1.5rem !important;
}
header{
  background: #0f4583 url(https://img.fifa.com/image/upload/t_fe-auto/assets/img/tournaments/17/2018/common/fwc_darkbluebg.png) repeat;
  background-size: cover;
  color: white;
  height: 20vh;
  padding: 15px;
}
.container {
  display: flex;
  align-items: center;
  justify-content: center;
}
.button{
  color: blanchedalmond !important;
  margin: 5px;
}
.button:hover{
  background-color: blanchedalmond !important;
  border-color: #0f4583 !important; 
  color: #0f4583 !important;
}
a{
  text-decoration: none !important;
  color: blanchedalmond !important;
}
a:hover{
  color: #0f4583 !important;
  text-decoration: none !important;
}
</style>
