<template>
  <div id="wrapper">
    <!-- Google Map On Construction -->
    <div v-if="isLoadingFriends">
      <!-- TODO: use common loading dots -->
      isLoadingFriends...
    </div>
    <div v-else>
      <GoogleMap
        v-if="selectedFriend"
        v-bind:selectedFriend="selectedFriend"
        v-bind:handleBackButtonClick="handleBackButtonClick"  
      />
      <div v-if="selectedFriend">
        <FriendCard
          v-bind:friend="selectedFriend"
        />
      </div>
      <FriendCard
        v-if="!selectedFriend"
        :key="index"
        v-for="(friend, index) in friends"
        v-bind:friend="friend"
        v-bind:handleClick="handleFriendCardClick"
      />
    </div>
  </div>
</template>

<script>
import { FRIENDS_LIST_ENDPOINT } from './constants';
import FriendCard from './components/FriendCard';
import GoogleMap from './components/GoogleMap';

export default {
  name: 'FriendsOnMapPage',
  el: '#friendsOnMap',
  components: {
    FriendCard,
    GoogleMap
  },
  data () {
    return {
      friends: [],
      selectedFriend: null,
      isLoadingFriends: true,
    }
  },
  created() {
    fetch(FRIENDS_LIST_ENDPOINT).then(response => response.json()).then(
      json => {
        this.friends = json,
        this.isLoadingFriends = false
      }
    );
  },
  methods: {
    handleFriendCardClick: function(friend) {
      this.selectedFriend = friend;
    },
    handleBackButtonClick: function() {
      this.selectedFriend = null;
    }
  }
}
</script>

<style>
  #wrapper {
    max-width: 600px;
    margin: 0 auto;
  }
</style>

