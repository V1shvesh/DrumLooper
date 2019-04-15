<template>
    <BeatMatrix />
</template>

<script>
import BeatMatrix from './components/BeatMatrix.vue';

export default {
  name: 'app',
  components: {
    BeatMatrix,
  },
};
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
