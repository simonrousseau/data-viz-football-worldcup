<template>
    <div class="container">
        <button v-if="detailsDisplayed" id="back" type="button" class="btn btn-primary" @click="back()">Back</button>
        <div id="fifaRank" v-if="!detailsDisplayed">
          <h2>Fifa Rank:</h2>
          <i>click on a team bar to display more information</i>
          <Chart  :chartdata="datacollection" :options="options" :width="1200" :height="600" id="chart"/>
        </div>
        <Teams v-if="detailsDisplayed" :team="selectedCountry" :players="players" />
    </div>
    
</template>

<script>
import Chart from './Chart.vue';
import Teams from './Teams.vue';

export default {
  name: "Players",
  components: {
      Chart,
      Teams
  },
  data: function() {
    return {
        selectedCountry: null,
        detailsDisplayed: false
    };
  },
  props: ["players"],
  methods: {
    displaySecond(e, ctx) {
        var xLabel = ctx.lastActive[0]._view.label;
        // eslint-disable-next-line no-console
        console.log(ctx.lastActive[0]._view.label);
        this.detailsDisplayed = true;
        this.selectedCountry = xLabel;
      
    },
    back() {
      // eslint-disable-next-line no-console
      console.log("Back");
      this.detailsDisplayed = false;
      this.selectedCountry = null;
    }
  },
  computed:{
      listPlayers: function(){
        var temp = [];
        this.players.map(p => {
            temp.push(p)
        })
        return temp;
      },
      classement: function(){
        var temp = {}
        this.players.map(p => {
            temp[p.Team] = p.Points
        })
        return temp;
      },
      team: function(){
        var temp = {}
        this.players.map(p => {
            temp[p.Team] = p.Team
        })
        return Object.values(temp);
      },
      points: function(){
          var temp = {}
            this.players.map(p => {
                temp[p.Team] = p.Points
            })
            return Object.values(temp);
      },
      datacollection: function() {
          return {
				labels: this.team,
				datasets: [
					{
						label: 'Fifa points',
						backgroundColor: '#0f4583',
						pointBackgroundColor: 'white',
						borderWidth: 1,
						pointBorderColor: '#0f4583',
						data: this.points
					}
]
			}
      },
      options: function() {
      var _this = this;
      return {
        onClick: function(evt) {
          _this.displaySecond(evt, this);
        }
      };
    },
    }
  }
</script>

<style scoped>
#back{
  position: absolute;
  top: 10px;
  left: -50px;
  background-color: #0f4583;
  border-color: #0f4583;
}
.container{
  position: relative;
  height: 80vh;
  width: 100%
}
#fifaRank{
  margin-top: 100px;
}
</style>