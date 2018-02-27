<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: "App"
};
</script>

<style lang="sass">
@import 'theme'
@import '../node_modules/bulma/css/bulma.css' 

html
  height: 100vh
  width: 100vw
  background: #4B79A1
  background: -webkit-linear-gradient(to right, #283E51, #4B79A1)
  background: linear-gradient(to right, #283E51, #4B79A1)
  

</style>
