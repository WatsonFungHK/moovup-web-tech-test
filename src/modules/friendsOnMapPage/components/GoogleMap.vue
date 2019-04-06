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
        v-if="hasLatAndLng"
        :position="location"
        :clickable="true"
        :draggable="true"
        @click="center=location"
      />
    </GmapMap>
    <div v-if="!hasLatAndLng" class="error-message">Can not locate this person</div>
  </div>
</template>

<script>
import { DEFAULT_GOOGLE_MAP_POSITION } from '../constants';

export default {
  name: 'GoogleMap',
  props: {
    selectedFriend: Object,
    handleBackButtonClick: Function
  },
  computed: {
    hasLatAndLng: function() {
      const { latitude, longitude } = this.selectedFriend.location;
      return latitude && longitude;
    },
    location: function() {
      try {
        if (!this.hasLatAndLng) {
          throw new Error('Lack of latitude or/and longitude');
        }
        const { latitude, longitude } = this.selectedFriend.location;
        return {
          lat: latitude,
          lng: longitude
        };
      } catch (exception) {
        // TODO: log to centralized error log
        return DEFAULT_GOOGLE_MAP_POSITION;
      }
    }
  }
}
</script>

<style>
  .map {
    width: 100%;
    height: 300px;
  }
  .back-button {
    margin: 16px 0;
    padding: 8px 16px;
    border-radius: 4px;
    box-shadow: 0 1px 2px 0 rgba(0, 0 , 0, 0.2);
  }
  .error-message {
    font-size: 14px;
    color: red;
    margin: 8px 0;
  }
</style>

