<template>
<div>
<div class="list-property">
          <div class="list-row-item"> <div class="list-property-name">Meeting Name </div>  {{racesData.meeting_name}} </div>
          <div class="list-row-item"><div class="list-property-name"> Race Number  </div>{{racesData.race_number}} </div>
        <div class="list-row-item"><div class="list-property-name"> Race Countdown  </div>{{countdown.minutes}} m {{countdown.seconds}} s </div>
</div>
</div>
</template>

<script>
export default {
  name: 'RacePanel',
  props: ['racesData', 'index'],
  computed: {
      countdown: function () {
      /** Countdown timer the race to start**/
      const delta = this.countTimeTarget - this.currentTime;
          const minutes = Math.floor(delta/60000);
          const seconds = Math.round(delta % 60000/1000);
          /** Wait for 60 seconds **/
         if (delta > -60000) {
           return {minutes:minutes, seconds:seconds};
         } else {
             // if countdown is > 60 secs
             //  destroy the interval
             //emit the value to raceList component
             this.$emit('remove');
             return { minutes:0, seconds:0 };
         }
}
  },
  data() {
  return {
     countTimeTarget: 0,
     currentTime: 0
 }
  },
  mounted: function () {
        const self = this;
         this.countTimeTarget = this.racesData.advertised_start.seconds * 1000;
         setInterval(function () {
            self.currentTime = Date.now();
        }, 1000 )
    }
}
</script>

<style scoped>
.list-property {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.list-property-name {
    font-weight: bold;
    transition: all 0.5s;
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
