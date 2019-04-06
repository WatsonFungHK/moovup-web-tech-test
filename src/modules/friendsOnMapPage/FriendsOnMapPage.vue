<template>
  <div id="friendsOnMap">
    <GmapMap
      v-if="location"
      style="width: 500px; height: 300px"
      :center="location"
      :zoom="10"
      map-type-id="terrain"
    >
      <GmapMarker
        :key="index"
        v-if="!isNaN(selectedFriendIndex)"
        :position="location"
        :clickable="true"
        :draggable="true"
        @click="center=location"
      />
    </GmapMap>
    <div v-if="isLoadingFriends">
      <!-- TODO: use common loading dots -->
      isLoadingFriends...
    </div>
    <div v-else>
      <div v-if="!isNaN(selectedFriendIndex)">You are viewing {{ friends[selectedFriendIndex].name.first }} {{ friends[selectedFriendIndex].name.last }}.</div>
      <div class="friend-card" v-for="(friend, index) in friends" :key="index" v-on:click="handleFriendCardClick(friend, index)">
        <span class="avatar">
          <!-- TODO: use people avatar instead of vue logo -->
          <img class="avatar-img" src="../../assets/logo.png" />
        </span>
        <span class="friend-info-wrapper">
          <div class="friend-name">
            {{ friend.name.first }} {{ friend.name.last }}
          </div>
          <div class="friend-email">
            {{ friend.email }}
          </div>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import { FRIENDS_LIST_ENDPOINT, INITIAL_LOCATION } from './constants';

export default {
  name: 'FriendsOnMapPage',
  el: '#friendsOnMap',
  data () {
    return {
      selectedFriendIndex: NaN,
      location: INITIAL_LOCATION,
      isLoadingFriends: true,
      friends: [],
      markers: []
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
    handleFriendCardClick: function(friend, index) {
      this.selectedFriendIndex = index;
      this.location = { lat: friend.location.latitude, lng: friend.location.longitude };
    }
  }
}
</script>

<style>
  #friendsOnMap {
    max-width: 500px;
    margin: 0 auto;
  }
  .friend-card {
    box-sizing: border-box;
    margin: 16px 0;
    padding: 16px;
    background-color: #f5f5f5;
    border-radius: 4px;
    box-shadow: 0 2px 4px 0 rgba(0, 0 , 0, 0.2);
    width: 100%;
    cursor: pointer;
  }
  .avatar {
    margin-right: 16px;
  }
  .avatar-img {
    vertical-align: middle;
    height: 50px;
    width: 50px;
  }
  .friend-info-wrapper {
    vertical-align: middle;
    display: inline-block;
  }
  .friend-name {
    font-weight: bold;
  }
  .friend-email {
    font-size: 14px;
  }
  .vue-map-container,
  .vue-map-container .vue-map {
    width: 100%;
    height: 100%;
  }
</style>

