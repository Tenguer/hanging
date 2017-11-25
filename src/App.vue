<template>
  <div id="app">
    <Hanging/>
  </div>
</template>

<script>
import Hanging from './components/Hanging'

export default {
  name: 'app',
  components: {
    Hanging
  }
}
</script>

<style>
  body {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
</style>
