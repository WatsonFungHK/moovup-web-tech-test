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
        v-if="!locationError"
        :position="location"
        :clickable="true"
        :draggable="true"
        @click="center=location"
      />
    </GmapMap>
    <div v-if="locationError" class="error-message">{{ locationError }} </div>
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
  data() {
    return {
      locationError: ''
    };
  },
  computed: {
    location: function() {
      try {
        const { latitude, longitude } = this.selectedFriend.location;
        if (!latitude || !longitude) {
          throw new Error('Can not locate this person');
        }
        return {
          lat: latitude,
          lng: longitude
        };
      } catch (exception) {
        // TODO: log to centralized error log
        this.locationError = exception.message;
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

