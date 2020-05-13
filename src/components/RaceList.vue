<template>
  <div class="raceList">
  <div class="filters">
    <span class="filter" v-bind:class="{ active: currentFilter === 'ALL' }" v-on:click="setFilter('ALL')">ALL</span>
    <span class="filter" v-bind:class="{ active: currentFilter === 'Greyhound' }" v-on:click="setFilter('Greyhound')">Greyhound Racing</span>
    <span class="filter" v-bind:class="{ active: currentFilter === 'Harness' }" v-on:click="setFilter('Harness')">Harness Racing</span>
    <span class="filter" v-bind:class="{ active: currentFilter === 'Horse' }" v-on:click="setFilter('Horse')">Horse Racing</span>
  </div>
  <div class="projects">
		<div class="list-row" v-if="currentFilter === races.values.category_name || currentFilter === 'ALL'" v-bind:key="races.key" v-for="(races, index) in racesToDisplays">
                <RacePanel :races-data="races.values" :index="index" v-on:remove="removeRace"> </RacePanel>
    </div>
</div>
  </div>
</template>

<script>
import RacePanel from './RacePanel.vue'
export default {
  name: 'RaceList',
  components:{
  RacePanel
  },
  data () {
    return {
    currentFilter: 'ALL',
    races:[],
    category_name:'',
    }
  },
  methods: {
   // Set current filter
		setFilter: function(filter) {
			this.currentFilter = filter;
		},
    removeRace: function(){
    // remove from races array
      this.races.splice(0,1);
    }
	},
  computed: {
  racesToDisplays: function () {
  // sort in ascending order and limit the data to 5 every time loaded
    return this.races.sort((a, b) => new Date(a.values.advertised_start.seconds) - new Date(b.values.advertised_start.seconds)).slice(0,5)
  }
  },
  // API Call to get all the next races
  created() {
     this.$http.get('https://api.neds.com.au/rest/v1/racing/?method=nextraces&count=20')
     .then((data) => {
     if(data.status == 200) {
      const dataObject = data.data.data.race_summaries;
      Object.keys(dataObject).map(x => {
      // Match the key against the category_id
      if(dataObject[x].category_id == '9daef0d7-bf3c-4f50-921d-8e818c60fe61') {
          this.category_name = 'Greyhound';
      }
      if(dataObject[x].category_id == '161d9be2-e909-4326-8c2c-35ed71fb460b') {
          this.category_name = 'Harness';
      }
      if(dataObject[x].category_id == '4a2788f8-e825-4d36-9894-efd4baf1cfae') {
          this.category_name = 'Horse';
      }
       Object.assign(dataObject[x], {category_name : this.category_name});
       /** Push all the data of races with key and value **/
      this.races.push({
            key: x,
            values:dataObject[x]
        })});

      } else {
          console.log('No Data found for the API or HTTP Error')
      }
     },(err) => {
        console.log(err);
     })
     .catch((e) => {
        console.log("Caught", e);
      })
  },
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.filter {
	font-family:arial;
	padding: 2px;
	cursor:pointer;
	border-radius: 6px;
	transition: all 0.35s;
}

.filter.active {
	box-shadow:0px 1px 3px 0px #00000026;
}
.filter:hover {
	background:lightgray;
}
.projects {
	margin-bottom:50px;
	margin-top:25px;
	display:flex;
	flex-wrap:wrap;
	justify-content:center;
}
.list-row {
    padding: 10px;
    margin: 10px;
    background: white;
    border-radius: 6px;
    -webkit-box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.37);
    -moz-box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.37);
    box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.37);
    display: grid;
    grid-template-columns:  1fr;
    width: 600px;
}
.list-row-item {
    display: grid;
    grid-template-columns: 150px 1fr;
    padding: 4px;
    transition: all 0.5s;
}
</style>
