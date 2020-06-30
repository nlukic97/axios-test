<template>
  <div id="app">
    <Fruits :colorFilter="this.colorFilter"/>
  </div>
</template>

<script>
import Fruits from './components/Fruits.vue'

export default {
  name: 'App',
  components: {
    Fruits
  },
  data(){
    return {
      // fruits: null
      colorFilter:"yellow"
    }
  },
  mounted(){
    
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
