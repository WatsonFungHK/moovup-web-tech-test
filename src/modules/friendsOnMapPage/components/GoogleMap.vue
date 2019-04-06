<template>
  <div>
    <button class="back-button" v-on:click="handleBackButtonClick">Back</button>
    <GmapMap
      class="map"
      :center="location"
      :zoom="10"
      map-type-id="terrain"
    >
      <GmapMarker
        v-if="selectedFriend"
        :key="selectedFriend._id"
        :position="location"
        :clickable="true"
        :draggable="true"
        @click="center=location"
      />
    </GmapMap>
  </div>
</template>

<script>
import { INITIAL_LOCATION } from '../constants';

export default {
  name: 'GoogleMap',
  props: {
    selectedFriend: Object,
    handleBackButtonClick: Function
  },
  computed: {
    location: function() {
      try {
        return {
          lat: this.selectedFriend.location.latitude,
          lng: this.selectedFriend.location.longitude
        };
      } catch {
        return INITIAL_LOCATION
      }
    }
  }

}
</script>

<style>
  .map {
    width: 500px;
    height: 300px;
  }
  .back-button {
    margin: 16px 0;
    padding: 8px 16px;
    border-radius: 4px;
    box-shadow: 0 1px 2px 0 rgba(0, 0 , 0, 0.2);
  }
</style>

