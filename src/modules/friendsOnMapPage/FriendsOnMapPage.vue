<template>
  <div id="friendsOnMap">
    <div v-if="isLoadingFriends">
      <!-- TODO: use common loading dots -->
      isLoadingFriends...
    </div>
    <div v-else>
      <div class="friend-card" v-for="friend in friends">
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
import { FRIENDS_LIST_ENDPOINT } from './constants';

export default {
  el: '#friendsOnMap',
  data () {
    return {
      isLoadingFriends: true,
      friends: []
    }
  },
  created() {
    fetch(FRIENDS_LIST_ENDPOINT).then(response => response.json()).then(
      json => {
        this.friends = json,
        this.isLoadingFriends = false
        }
    );
  }
}
</script>

<style>
  #friendsOnMap {
    max-width: 400px;
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
</style>

