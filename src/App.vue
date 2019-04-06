<template>
  <div id="app">
    <FriendsMap />
  </div>
</template>

<script>
import FriendsMap from './modules/friendsOnMapPage';

export default {
  name: 'app',
  components: {
    FriendsMap
  }
}
</script>

<style>
#app {
  font-family: 'Lato', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
