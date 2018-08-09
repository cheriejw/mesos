<template>
  <div id="app">
    <DataCenterManagement/>
  </div>
</template>

<script>
import DataCenterManagement from '@/components/DataCenterManagement.vue';

export default {
  name: 'app',
  components: {
    DataCenterManagement
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
