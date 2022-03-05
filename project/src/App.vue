<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  
  <!-- <graphup :data_time = data_up :data_dif = data_down> </graphup> -->
  <RunPosition></RunPosition>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import graphup from './components/graphup.vue'
import RunPosition from './components/RunPosition.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    graphup,
    RunPosition
  },
  data(){
    return{
      data_up:[0.1,0.1,0.05,0.1,0.1,0.2,0.05,0.1,0.1,0.1],
      data_down:[0.1,0.1,0.05,0.1,0.1,0.2,0.05,0.1,0.1,0.1]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
