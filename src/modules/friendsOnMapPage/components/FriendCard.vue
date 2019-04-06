<template>
  <div class="card-wrapper" v-on:click="handleClick(friend)">
    <span class="avatar">
      <!-- TODO: use people avatar instead of vue logo -->
      <img class="avatar-img" src="../../../assets/logo.png" />
    </span>
    <span class="basic-info-wrapper">
      <div class="friend-full-name">
        {{ friend.name.first }} {{ friend.name.last }}
      </div>
    </span>
    <div v-if="isSelected">
      <div class="friend-detail-info">id: {{ friend._id }}</div>
      <div class="friend-detail-info">email: {{ friend.email }}</div>
      <div class="friend-detail-info">picture: {{ friend.picture }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FriendCard',
  props: {
    friend: Object,
    handleClick: Function,
    isSelected: Boolean
  }
}
</script>

<style>
  .card-wrapper {
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
  .basic-info-wrapper {
    vertical-align: middle;
    display: inline-block;
  }
  .friend-detail-info {
    margin: 16px 32px;
  }
  .friend-full-name {
    font-weight: bold;
  }
</style>


