<template>
  <div id="app">
  <app-header></app-header>
    <RaceList/>
    <app-footer></app-footer>
  </div>
</template>

<script>
import RaceList from './components/RaceList.vue'
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
export default {
  name: 'App',
  components: {
    RaceList,
    'app-header':Header,
    'app-footer':Footer
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
}

* {
margin: 0;
padding: 0;
}
</style>
