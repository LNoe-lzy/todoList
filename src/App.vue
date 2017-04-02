<template>
  <div id="app">
    <Todos></Todos>
  </div>
</template>

<script>
import Todos from './components/Todos'

export default {
  components: {
    Todos
  }
}
</script>

<style>
#app {
  margin: 0 auto;
  width: 400px;
}
</style>
