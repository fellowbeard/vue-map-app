<template>
  <div class="about">
    <h1>This is a map</h1>
    <div id="map"></div>
  </div>
</template>
<script>
/* global mapboxgl */
export default {
  data: function () {
    return {
      places: [],
    };
  },
  mounted: function () {
    this.getPlaces();
  },
  methods: {
    getPlaces() {
      // make axios
      this.places = [{ lat: 19.590414, lng: -154.948261, description: "Me!" }];
      this.setMap();
    },
    setMap() {
      mapboxgl.accessToken = process.env.VUE_APP_MAP_API_KEY;
      const map = new mapboxgl.Map({
        container: "map", // container ID
        style: "mapbox://styles/mapbox/streets-v11", // style URL
        center: [this.places[0].lng, this.places[0].lat], // starting position [lng, lat]
        zoom: 9, // starting zoom
      });
      this.places.forEach((place) => {
        // create the popup
        const popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
        // Create a default Marker and add it to the map.
        const marker = new mapboxgl.Marker().setLngLat([place.lng, place.lat]).setPopup(popup).addTo(map);
        console.log(map, marker);
      });
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#map {
  width: 100%;
  height: 50vh;
}
</style>
