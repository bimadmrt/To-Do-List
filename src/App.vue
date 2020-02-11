<template>
  <div id="app">  
    <Todolist />
  </div>
</template>

<script>
import Todolist from './components/Todolist.vue';

export default {
  name: 'App',
  components: {
    Todolist,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  background-color: pink;
  margin-top: 60px;
}
</style>