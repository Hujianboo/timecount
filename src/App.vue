<template>
  <div id="app">
    <!-- coutDown的传入参数为毫秒 -->
    <countDown :time ="5*60000" @end="handler"></countDown> 
    <countDown :time ="2*6000" @end="handler"></countDown>
    <countDown :time ="3*6000" @end="handler"></countDown>
  </div>
</template>

<script>
import countDown from './components/countDown'

export default {
  name: 'App',
  components: {
    countDown
  },
  methods:{
    handler(...args){
        console.log(...args);
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
