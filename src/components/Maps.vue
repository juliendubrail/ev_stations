<template>
<div>
  <h2>Car Location</h2>
      <Example></Example>
</div>
</template>

<script>

import Example from "./Example";
export default {
  components: {
    Example
  },
  computed: {
    mapConfig () {
      return {
        mapSettings: {
          enableHighAccuracy: true,
          timeout: 5000,
          maximumAge: 0
        },
        zoom: 15,
        center: { lat: parseInt(this.$route.params.lat, 0), lng: parseInt(this.$route.params.lng, 0) }
      }
    },
  }
};
</script>