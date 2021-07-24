<template>
  <l-map :zoom="zoom" :center="center" style="height: 98vh; width: 100%">
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
        '&copy; <a target="_blank" href="https://www.linkedin.com/in/mustafa-erk-548a32126/">Mustafa ERK</a> contributors',
      icon: icon({
        iconUrl: MarkerIcon,
        iconSize: [24, 30],
        iconAnchor: [12, 15],
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


