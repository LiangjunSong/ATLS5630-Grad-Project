<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Search
    @test="testFunction"
    />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Search from './components/Search'

export default {
  name: 'app',
  components: {
    HelloWorld,
    Search
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
