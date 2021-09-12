<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col
            cols="12"
            sm="4"
          >
            <place-search @cityselected="citySelected" />          
          </v-col>
          <v-col
            cols="12"
            sm="4"
          >
            <place-popular :popularCities="popularCities" />          
          </v-col>
          <v-col
            cols="12"
            sm="4"
          >
            <place-result />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import PlaceSearch from './components/PlaceSearch.vue';
import PlacePopular from './components/PlacePopular.vue';
import PlaceResult from './components/PlaceResult.vue';

export default {
  name: 'App',

  components: {
    PlaceSearch,
    PlacePopular,
    PlaceResult
  },

  data: () => {
    return {
      popularCities: []
    }
  },

  mounted() {
    let popularCities = window.localStorage.getItem('weatherApp_popularCities');
    if (popularCities) {
      try {
        this.popularCities = JSON.parse(popularCities);
      } catch (e) {
        console.warn('Error with parsing data from local storege:', e);
      }
    } else {
      this.popularCities = [
        'Дніпро',  'Київ', 'Львів', 'London', 'Los Angeles', 'New York'
      ]
    }
  },

  methods: {
    citySelected (city) {
      console.log(city)
    }
  }
};
</script>

<style>
main {
  background-image: url('./assets/clouds.jpg');
  background-size: cover;
}
</style>