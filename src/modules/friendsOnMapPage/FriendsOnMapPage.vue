<template>
  <div id="wrapper">
    <div v-if="isLoadingFriends" class="loading-message">
      is loading friends...
    </div>
    <div v-else>
      <GoogleMap
        v-if="selectedFriend"
        v-bind:selectedFriend="selectedFriend"
        v-bind:handleBackButtonClick="handleBackButtonClick"  
      />
      <div v-if="selectedFriend">
        <FriendCard v-bind:friend="selectedFriend" isSelected="true" />
      </div>
      <div v-else>
        <FriendCard
          :key="index"
          v-for="(friend, index) in friends"
          v-bind:friend="friend"
          v-bind:handleClick="handleFriendCardClick"
        />
      </div>
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
  .loading-message {
    text-align: center;
  }
</style>

