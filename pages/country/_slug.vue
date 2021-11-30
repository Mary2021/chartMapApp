<template>
<div>
    <v-row>
   <v-btn class='ma-2' @click="dataLabel='confirmed'">Confirmed</v-btn>
   <v-btn class='mt-2' @click="dataLabel='deaths'">Deaths</v-btn>

    <v-col
      cols="12"
      sm="6"
      md="4"
      class="pa-1"
    >
      <v-menu
        ref="menuStart"
        v-model="menuStart"
        :close-on-content-click="false"
        :return-value.sync="startDate"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="startDate"
            label="Select start date"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="startDate"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="menuStart = false"
          >
            Cancel
          </v-btn>
          <v-btn
            id="okStart"
            text
            color="primary"
            @click="$refs.menuStart.save(startDate)"
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>

    <v-col
      cols="12"
      sm="6"
      md="4"
      class="pa-1"
    >
      <v-menu
        ref="menuEnd"
        v-model="menuEnd"
        :close-on-content-click="false"
        :return-value.sync="endDate"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="endDate"
            label="Select end date"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker
          v-model="endDate"
          no-title
          scrollable
        >
          <v-spacer></v-spacer>
          <v-btn
            text
            color="primary"
            @click="menuEnd = false"
          >
            Cancel
          </v-btn>
          <v-btn
            text
            color="primary"
            @click="$refs.menuEnd.save(endDate)" 
          >
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>
    <v-btn class='mt-2' @click="getCountry">Update</v-btn>
    </v-row>
    <chart :data="$store.getters[dataLabel]" :labels="$store.getters.labels" :dataLabel="dataLabel"></chart>
</div>
</template>

<script>
import Chart from '~/components/Chart.vue';
export default {
    components: { Chart },
    created(){
        let chartObject = {slug: this.$route.params.slug, startDate: this.startDate, endDate: this.endDate};
        this.$store.dispatch('getCountry', chartObject);
    },
    data(){
        const current = new Date();
        const prior = new Date().setDate(current.getDate() - 30);
        return {
            dataLabel: 'confirmed',
            startDate: (new Date(prior - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menuStart: false,
            endDate: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substr(0, 10),
            menuEnd: false,
        }    
    },
    methods: {
      getCountry(){
        let chartObject = {slug: this.$route.params.slug, startDate: this.startDate, endDate: this.endDate};
        this.$store.dispatch('getCountry', chartObject);
      }
    }
}
</script>


<style>

</style>