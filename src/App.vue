<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Search
    @test="testFunction"
    />
    <Playlist />
  </div>
</template>

<script>

import Search from './components/Search'
import Playlist from './components/Playlist'

export default {
  name: 'app',
  components: {
    Search,
    Playlist
  },
  methods: {
    testFunction(name) {
      console.log(name);
    }
  }
}
</script>

<style>
/*#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
