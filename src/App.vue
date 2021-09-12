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
            <place-popular
              @cityselected="popularSelected"
              :popularCities="popularCities" />
          </v-col>
          <v-col
            cols="12"
            sm="4"
          >
            <place-result :weather="weather" />
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
import axios from "axios";

const CITIES_LIST_KEY = 'weatherApp_popularCities';
const WEATHER_API_KEY = '121baa8610mshc64e99539dac27cp1d56fejsna1658398d71f';

export default {
  name: 'WeatherApp',

  components: {
    PlaceSearch,
    PlacePopular,
    PlaceResult
  },

  data: () => {
    return {
      popularCities: [],
      weather: {},
      selectedCity: {}
    }
  },

  mounted() {
    let popularCities = window.localStorage.getItem(CITIES_LIST_KEY);

    if (popularCities) {
      try {
        this.popularCities = JSON.parse(popularCities);
      } catch (e) {
        console.warn('Error with parsing data from local storege:', e);
      }
    } else {
      this.popularCities = [
        { name: 'Дніпро', lat: 48.46, lng: 35.05 },
        { name: 'Київ', lat: 50.45, lng: 30.52 },
        { name: 'Львів', lat: 49.84, lng: 24.03 },
        { name: 'London', lat: 51.51, lng: -0.13 },
        { name: 'Los Angeles', lat: 34.05, lng: -118.24 },
        { name: 'New York', lat: 40.71, lng: -74.01 }
      ]
    }
  },

  methods: {
    citySelected(data) {
      this.selectedCity = {
        name: data.locality,
        lat: data.latitude,
        lng: data.longitude
      };
      this.addCity(this.selectedCity);
      this.getWeather(this.selectedCity);
    },

    popularSelected(data) {
      this.selectedCity = data;
      this.getWeather(this.selectedCity);
    },

    addCity(data) {
      if (!this.popularCities.some(item => item.name === data.name)) {
        this.popularCities.shift();
        this.popularCities.push({
          name: data.name,
          lat: data.lat,
          lng: data.lng
        });
        window.localStorage.setItem(CITIES_LIST_KEY, JSON.stringify(this.popularCities));
      }
    },

    getWeather(data) {
      const options = {
        method: 'GET',
        url: 'https://weatherbit-v1-mashape.p.rapidapi.com/current',
        params: { lat: data.lat, lon: data.lng, units: 'metric' },
        headers: {
          'x-rapidapi-host': 'weatherbit-v1-mashape.p.rapidapi.com',
          'x-rapidapi-key': WEATHER_API_KEY
        }
      };

      axios.request(options).then(res => {
        this.weather = res.data.data[0];
      }).catch(err => {
        console.error(err);
      });
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