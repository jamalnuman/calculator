<template>
  <div id="app">
    <Calculator/>
    <router-view/>
  </div>
</template>

<script>
  import  Calculator from './components/Calculator.vue'

  export default {
    name: 'app',
    components: {
      Calculator
    }
  }

</script>

<style>

</style>
