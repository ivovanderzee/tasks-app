<template>
  <div id="app">
  <!-- import the task component in the body of the app -->
    <Tasks/>
  </div>
</template>

<script>
import Tasks from './components/Tasks.vue'

export default {
  name: 'app',
  components: {
    Tasks
  }
}
</script>

<style>

body {
  background-color: #EEEEEE;
  font-family: 'Montserrat', sans-serif;
  display: grid;
  grid-template-rows: auto;
  justify-items: center;
  align-items: center;
}
body, html {
  margin: 0;
  height: 100%;
}
#app {
    width: 50%;
}

</style>
