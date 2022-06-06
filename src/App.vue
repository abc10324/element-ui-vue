<template>
  <div id="app">
    <hello-world v-if="view == '1'"/>
    <select-view v-else-if="view == '2'"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import SelectView from './components/SelectView.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    SelectView
  },
  data(){
    return {
      view: "2"
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}
</style>
