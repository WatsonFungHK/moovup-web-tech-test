<template>
  <div id="app">
    <FriendsOnMapPage />
  </div>
</template>

<script>
import FriendsOnMapPage from './modules/friendsOnMapPage/FriendsOnMapPage';

export default {
  name: 'app',
  components: {
    FriendsOnMapPage
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
