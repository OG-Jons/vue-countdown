<template>
  <div id="app">
    <Countdown :end-date="new Date('2022-10-02')" />
    <Countdown :end-date="new Date('2022-04-15')" />
  </div>
</template>

<script>
import Countdown from "@/components/Countdown";
export default {
  name: 'App',
  components: {
    Countdown,
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
