<template>
  <div id="app">
    <NavBar/>
    <FruitList/>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import FruitList from './components/FruitList.vue'

export default {
  name: "app",
  components: {
    NavBar,
    FruitList
  }
};
</script>
<style>
  #app {
    font-family: Times, "Times New Roman", Georgia, serif;
    color :#222f3e!important;
  }
</style>

