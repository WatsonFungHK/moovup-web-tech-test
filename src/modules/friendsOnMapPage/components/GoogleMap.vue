<template>
  <div>
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
    selectedFriend: Object
  },
  computed: {
    location: function() {
      return this.selectedFriend ? {
        lat: this.selectedFriend.location.latitude,
        lng: this.selectedFriend.location.longitude
      } : INITIAL_LOCATION
    }
  }

}
</script>

<style>
  .map {
    width: 500px;
    height: 300px;
  }
</style>

