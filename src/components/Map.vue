<template>
  <div style="height: 1500px">
    <div style="height: 200px overflow: auto;">
      <p>current zoom {{ zoom }}</p>
    </div>
    <l-map
      :zoom="zoom"
      :center="center"
      style="height: 80%"
      @update:zoom="zoomUpdate"
      :options="mapOptions"
      @update:center="centerUpdate"
    >
      <l-tile-layer :url="url" :attribution="attribution" />
      <v-marker-cluster >
        <l-marker
          v-for="fountain in fountains"
          :key="fountain.id"
          :lat-lng="fountain.coords"
        >
          <l-popup> 
            <!-- some html stuff -->
            <p>Fountain Name: {{fountain.name}}</p>
            <p>Fountain link: <a :href="fountain.url" target="_blank">link</a> </p>
          </l-popup>
        </l-marker>
      </v-marker-cluster>
    </l-map>
  </div>
</template>

<script>
import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker, LPopup, LTooltip } from "vue2-leaflet";
import Vue2LeafletMarkerCluster from "vue2-leaflet-markercluster";

export default {
  name: "Map",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LTooltip,
    "v-marker-cluster": Vue2LeafletMarkerCluster,
  },
  data() {
    return {
      zoom: 7,
      //   center: latLng(46.927319, 8.544203),
      center: {
        lat: 46.927319,
        lon: 8.544203,
      },
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      withPopup: latLng(46.927319, 8.544203),
      // currentZoom: 11.5,
      // currentZoom: 5,
      currentCenter: latLng(47.41322, -1.219482),
      minZoom: 18,
      // clusterOptions: {},
      fountains: [
        {
          id: 0,
          coords: { lat: 46.927319, lon: 8.544203 },
          name: "a",
          description: ``,
          url: 'http://www.google.com'
        },
        {
          id: 1,
          coords: { lat: 46.927319, lon: 8.944205 },
          name: "b",
          description: "some other text",
          url: 'http://www.google.com'
        },
        {
          id: 2,
          coords: { lat: 46.442313, lon: 2.444950 },
          name: "c",
          description: "some other other text",
          url: 'http://www.google.com'
        },
        {
          id: 3,
          coords: { lat: 46.441731, lon: 2.447603 },
          name: "d",
          description: "some other other other text",
        },
        {
          id: 4,
          coords: { lat: 46.927319, lon: 8.543203 },
          name: "e",
          description: ``,
          url: 'http://www.google.com'
        },
      ],
      mapOptions: {
        // zoomSnap: 0.5,
      },
    };
  },
  methods: {
    zoomUpdate(zoom) {
      this.zoom = zoom;
    },
    centerUpdate(center) {
      this.currentCenter = center;
    },
  },
};
</script>

<style>
@import "~leaflet.markercluster/dist/MarkerCluster.css";
@import "~leaflet.markercluster/dist/MarkerCluster.Default.css";
</style>
