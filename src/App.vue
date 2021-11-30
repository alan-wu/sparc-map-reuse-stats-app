<template>
  <div id="app">
    <MapReuseStatsPage/>
  </div>
</template>

<script>
/* eslint-disable no-alert, no-console */
import MapReuseStatsPage from './components/MapReuseStatsPage.vue'

export default {
  name: 'app',
  components: {
    MapReuseStatsPage
  },
  data: function() {
    return {
      title: "Map Reuse Stats"
    }
  },
  created () {
    if (this.title) {
      document.title = this.title;
    }
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
  height:100%;
  width: 100%;
  position:absolute;
}

body {
  margin: 0px;
}

.boundary {
  width:500px;
  height:500px;
  top:100px;
  left:100px;
  background-color:thistle;
  position: absolute;
}

</style>
