<template>
<div>
  <v-row class="mt-1 mx-1">
    <v-text-field v-model="position.lat" label="Select latitude" type="number" dense filled class="col-2 mx-2"></v-text-field>
    <v-text-field v-model="position.lng" label="Select longitude" type="number" dense filled class="col-2 mx-2"></v-text-field>
    <v-btn class="mx-2" @click="position={lat:Number(position.lat), lng:Number(position.lng)}; zoom=4">Add marker</v-btn>
    <v-btn class="mx-2" @click="zoom=10">Zoom in</v-btn>
    <v-btn class="mx-2" @click="zoom=4">Zoom out</v-btn>
    <v-btn class="mx-2" @click="position={lat: 45, lng:25}; zoom=10">go to somewhere</v-btn>
  </v-row>
  <google-map :center="position" :zoom="zoom" :position="position">
  </google-map>
</div>
</template>

<script>
import GoogleMap from '~/components/GoogleMap.vue'

export default {
  components: { GoogleMap },

  data(){
    return {
        center: this.position,
        zoom: 4,
        position: {lat: 59.4717421, lng: 24.4580604}
      }
  },
}
</script>



<style>
   
</style>