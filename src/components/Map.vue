<template>
  <div>
    <l-map :zoom="zoom" :center="center" style="height: 500px; width: 100%">
      <l-tile-layer :url="url" :attribution="attribution" />

      <l-marker
        v-for="school in medicalSchoolsInfo"
        :key="school.NAME"
        :lat-lng="[school.LAT, school.LNG]"
        :icon="icon"
        @click="getCloserToSchool(school)"
      >
        <l-popup>
          <div>{{ school.NAME }}</div>
        </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import { latLng, icon } from "leaflet";
import { LMap, LMarker, LTileLayer, LPopup } from "vue2-leaflet";

import SchoolList from "../static/data/medical_schools.json";
import MarkerIcon from "../static/images/medicine-icon.png";

export default {
  name: "Map",
  components: {
    LMap,
    LMarker,
    LTileLayer,
    LPopup,
  },
  data() {
    return {
      zoom: 6,
      center: latLng(39.9207893, 32.8540412),
      url: "https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png",
      attribution:
        '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      icon: icon({
        iconUrl: MarkerIcon,
        iconSize: [24, 30],
        iconAnchor: [16, 30],
      }),
      medicalSchoolsInfo: [],
    };
  },
  mounted() {
    this.medicalSchoolsInfo = SchoolList;
  },
  methods: {
    getCloserToSchool(school) {
      this.center = latLng(school.LAT, school.LNG);
    },
  },
};
</script>

<style>
.someExtraClass {
  background-color: aqua;
  padding: 10px;
  border: 1px solid #333;
  border-radius: 0 20px 20px 20px;
  box-shadow: 5px 3px 10px rgba(0, 0, 0, 0.2);
  text-align: center;
  width: auto !important;
  height: auto !important;
  margin: 0 !important;
}
</style>
