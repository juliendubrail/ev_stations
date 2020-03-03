<template>

  <div style="height: 400px; width: 100%">
    <div style="height: 200px overflow: auto;">
      <p>First marker is placed at {{ withPopup.lat }}, {{ withPopup.lng }}</p>
      <p>Center is at {{ currentCenter }} and the zoom is: {{ currentZoom }}</p>
      <button @click="showLongText">
        Toggle long popup
      </button>
      <button @click="showMap = !showMap">
        Toggle map
      </button>
      <button @click="goBack">
          Go Back to List
      </button>
        <button @click="getUserLocation">
          Go to User Location
      </button>
    </div>
    <l-map
      ref="map"
      v-if="showMap"
      :zoom="zoom"
      :center="center"
      :options="mapOptions"
      style="height: 80%"
      @update:center="centerUpdate"
      @update:zoom="zoomUpdate"
    >
      <l-tile-layer
        :url="url"
        :attribution="attribution"
      />
      <l-marker :lat-lng="withTooltip">
        <l-tooltip :options="{ permanent: true, interactive: true }">
          <div @click="innerClick">
            I am a tooltip
            <p v-show="showParagraph">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Quisque
              sed pretium nisl, ut sagittis sapien. Sed vel sollicitudin nisi.
              Donec finibus semper metus id malesuada.
            </p>
          </div>
        </l-tooltip>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import router from '../router'
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LTooltip } from "vue2-leaflet";

export default {
  name: "Example",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LTooltip
  },
  data() {
    return {
      zoom: 13,
      center: latLng(this.$route.params.lat, this.$route.params.lng),
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      withPopup: latLng(this.$route.params.lat, this.$route.params.lng),
      withTooltip: latLng(this.$route.params.lat + 0.1, this.$route.params.lng + 0.1),
      currentZoom: 11.5,
      currentCenter: latLng(this.$route.params.lat, this.$route.params.lng),
      showParagraph: false,
      mapOptions: {
        zoomSnap: 0.5
      },
      showMap: true
    };
  },
  methods: {
    zoomUpdate(zoom) {
      this.currentZoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
    showLongText() {
      this.showParagraph = !this.showParagraph;
    },
    innerClick() {
      alert("Click!");
    },
    goBack(){
        router.push({name: 'List'})
    },
    flyTo(lat, lng){
      this.$refs.map.mapObject.flyTo([lat],[lng])
    },
    getUserLocation(){
      if(navigator.geolocation){
        navigator.geolocation.getCurrentPosition(({coords}) =>{
          this.flyTo(coords.latitude, coords.longitude);
        })
      }
    } 
  }
};
</script>
