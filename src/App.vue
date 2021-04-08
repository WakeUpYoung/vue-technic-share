<template>
  <div id="app" class="container">
    <NumberFlapper></NumberFlapper>
  </div>
</template>

<script>
import NumberFlapper from '@/components/NumberFlapper'

export default {
  name: 'App',
  components: {
    NumberFlapper
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
