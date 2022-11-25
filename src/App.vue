<template>
  <div id="app">
    <settingsScreen/>
  </div>
</template>

<script>
import settingsScreen from './views/Settings.vue'

export default {
  name: 'App',
  components: {
    settingsScreen
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Montserrat, Helvetica, Arial, sans-serif;
}

body {
  min-width: 320px;
}

#app {
  padding: 20px;
}

@media (max-width: 800px) {
  #app {
    padding: 8px;
  }
}
</style>
