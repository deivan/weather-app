<template>
    <v-card
        elevation="3"
        tile
    >
        <v-card-title>Weather results</v-card-title>
        <v-card-text v-if="weather.weather">
            <h3>{{weather.city_name}}</h3>
            <p>Clouds: {{weather.weather.description}}</p>
            <p>Temperature: {{weather.temp}}</p>
            <p>Sunrise time: {{weather.sunrise}}</p>
            <p>Sunset time: {{weather.sunset}}</p>
            <p>Wind speed: {{weather.wind_spd}}</p>
            <p>Wind direction: {{weather.wind_cdir_full}}</p>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    props: ['weather']
}
</script>

<style>

</style>