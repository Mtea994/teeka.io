<template>
  <div class="home">
    <l-map 
     v-model="zoom"
      v-model:zoom="zoom"
    :center="[34.0151, 71.5249]">
    <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      ></l-tile-layer>
       <l-marker :lat-lng="[34.0151, 71.5249]">
        <l-icon icon-url="https://image.flaticon.com/icons/png/512/101/101960.png" :icon-size="[24,24]" />
      </l-marker>
      <l-control-layers />
    </l-map>
  </div>
</template>

<script>
// @ is an alias to /src

import {
  LMap,
  LIcon,
  LTileLayer,
  LMarker,
  LControlLayers,
  LTooltip,
  LPopup,
  LPolyline,
  LPolygon,
  LRectangle,
} from "@vue-leaflet/vue-leaflet";
import { ref } from 'vue';

export default {
  name: 'Home',
  components: {
    LMap,
    LIcon,
    LTileLayer,
    LMarker,
    LControlLayers,
    LTooltip,
    LPopup,
    LPolyline,
    LPolygon,
    LRectangle,
  },
  setup(){
    const zoom = ref(11);
    const placesURL = 'https://cors-anywhere.herokuapp.com/https://www.google.com/maps/d/u/0/kml?mid=1k0P6q0dXgrsxHVUbDifuEyxxSz8xh6Hd&nl=1&forcekml=1';

    async function getProviders(){
      const response = await fetch(placesURL);
      const xml = await response.text();
      const dom = new DOMParser().parseFromString(xml, 'text/xml');
      const innerLink = dom.querySelector('Document NetworkLink Link href');
      const innerPlacesURL = innerLink.textContent;
      const innerResponse = await fetch(innerPlacesURL);
      const innerXML = await innerResponse.text();
     // const innerDOM = new DOMParser().parseFromString(innerXML, 'text/xml');

      console.log(innerXML);
    }
    getProviders();
    return {
      zoom,
    };
  },
};
</script>

<style lang="scss">
.home {
  width: 100%;
  height: 100%;
}

</style>
