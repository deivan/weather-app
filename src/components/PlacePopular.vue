<template>
  <v-card
        elevation="3"
        tile
    >
        <v-card-title>Popular cities</v-card-title>
        <v-card-text>
            <v-list-item v-for="item in popularCities" :key="item.name">
                <v-list-item-content>
                    <v-list-item-title>
                        <v-btn depressed @click="showWeather(item)">{{ item.name }}</v-btn>
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    props: ['popularCities'],

    methods: {
        showWeather(data) {
            this.$emit('cityselected', {
                name: data.name,
                lat: data.lat,
                lng: data.lng
            })
        }
    }
}
</script>

<style>

</style>