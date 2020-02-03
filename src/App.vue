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
      graphics:[{x:50,y:40},{x:100,y:200},{x:150,y:160},{x:200,y:240},{x:250,y:80},{x:300,y:120},{x:350,y:140},{x:400,y:120}]
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
