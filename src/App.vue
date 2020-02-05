<template>
  <div id="app">
    <graph :graphics='graphics' msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import graph from './components/Graph.vue'

export default {
  name: 'app',
  data() {
    return {
      graphics:[[40,200,20,700,40,200,160,240],[10,20,30,50,60,70,100,110]]
    }
  },
  
  components: {
    graph
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
  margin-top: 60px;
}
</style>
