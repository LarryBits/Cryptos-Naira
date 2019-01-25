<template>
  <div id="app">
    <app-header></app-header>
     <app-converter></app-converter>
  </div>
</template>

<script>
import Converter from './components/Converter.vue'
import Header from './components/Header.vue'


export default {
  name: 'app',
  components: {
    appConverter:Converter,
    appHeader:Header,
  }
}
</script>

<style>


</style>
