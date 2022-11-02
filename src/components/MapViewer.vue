<!-- <script setup>
import "leaflet/dist/leaflet.css"
import { ref } from 'vue';
defineProps({
    latlong: { type: Array, default: [22, 91] }
})

const zoom = ref(10)
const minzoom = ref(3)
function addPopUp() {
    console.log('POOP!!')
}
</script> -->

<script>
import "leaflet/dist/leaflet.css"
import { LMap } from "@vue-leaflet/vue-leaflet";

export default {
    props: {
        latlong: Array
    },
    components: {
        LMap,
    },
    data() {
        return {
        };
    },
    async beforeMount() {
        // HERE is where to load Leaflet components!
        // const { circleMarker } = await import("leaflet/dist/leaflet-src.esm");

        // // And now the Leaflet circleMarker function can be used by the options:
        // this.geojsonOptions.pointToLayer = (feature, latLng) =>
        //     circleMarker(latLng, { radius: 8 });
        // this.mapIsReady = true;
    },
};
</script>

<template>
    <h1>{{ latlong }}</h1>
    <div class="relative w-[600px] h-[600px] bg-green-100" id="mapContainer">
        <!-- <l-map ref="map" v-model="zoom" v-model:zoom="zoom" :center="latlong"
            :options="{ zoomControl: false, attributionControl: false }" :minZoom="minzoom" @click="addPopUp" /> -->
    </div>
</template>