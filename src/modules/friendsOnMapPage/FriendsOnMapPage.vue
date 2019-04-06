<template>
  <div id="friendsOnMap">
    <!-- Google Map On Construction -->
    <GoogleMap v-bind:selectedFriend="selectedFriend" />
    <div v-if="isLoadingFriends">
      <!-- TODO: use common loading dots -->
      isLoadingFriends...
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
        this.friends = json.filter(friend => friend.location.latitude && friend.location.longitude),
        this.isLoadingFriends = false
        }
    );
  },
  methods: {
    handleFriendCardClick: function(friend) {
      this.selectedFriend = friend;
    }
  }
}
</script>

<style>
  #friendsOnMap {
    max-width: 500px;
    margin: 0 auto;
  }
</style>

