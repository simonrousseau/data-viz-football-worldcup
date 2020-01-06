<template>
    <div class="container">
        <h2 id="pays">{{team}} <img v-bind:src="flag" alt="flag"></h2>
        <div id="tablePlayers">
            <b-table striped hover :items="listPlayers" :fields="fields" @row-clicked="myRowClickHandler">
            </b-table>
        </div>
        
        <Radar :chartData="rowData" :options="options"/>
        
    </div>
    
</template>


<script>
import Radar from './Radar.vue';

export default {
  name: "Teams",
  data() {
      return {
          fields: ['Player', 'Position', 'Age', 'Club','Goals','Assists', ],
          selectedPlayer: ""
      }
  },
  components: {
      Radar
  },
  props: [
    "team", "players"
  ],
  computed: {
      listPlayers: function() {
          return this.players.filter( e => {
              return e.Team == this.team;
          })
      },
      flag: function() {
          return this.listPlayers[0].Image;
      },
      rowData: function() {
          return {
                labels: ['Perfattack','Perfdef','Perfposs','Mins','Ps'],
                datasets: [{
                    data: [this.selectedPlayer.Perfattack, this.selectedPlayer.Perfdef, this.selectedPlayer.Perfposs, this.selectedPlayer.Mins ,this.selectedPlayer.Ps],
                    backgroundColor: 'rgba(15, 69, 131, 0.4)'
                }]
            }
        },
        options: function() {
            return {
                legend: {
                    display: false
                }
            }
    }
  },
  methods: {
      myRowClickHandler(record) {
        // eslint-disable-next-line no-console
        console.log(record);
        this.selectedPlayer = record;
    }
  }
}

</script>

<style scoped>
#pays{
    position: absolute;
    top: 10px;
}
.container{
  position: relative;
  height: 80vh;
  width: 100%
}
#tablePlayers{
    height: 80%;
    width: 100%;
    overflow: scroll;
    margin-right: 20px;
}
</style>