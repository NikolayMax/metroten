<template>
  <div id="app">
    <LeftMenu />
    <Router />
  </div>
</template>

<script>
import LeftMenu from './components/LeftMenu.vue';
import Router from './components/Router.vue';
import './assets/z-task/font-awesome-4.7.0/css/font-awesome.min.css';
import './assets/fonts.css';

export default {
  name: 'app',
  components: {
    LeftMenu,
    Router
  }
}
</script>

<style>
  body{
    margin: 0px;
    background-color: #f5f5f7;
  }
#app {
  font-family: 'Heebo-Regular', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
