<template>
    <v-card
        elevation="3"
        tile
    >
        <v-card-title>Search city</v-card-title>
        <v-card-text>
            <vue-google-autocomplete
                id="map"
                ref="toAddress"
                classname="form-control"
                placeholder="Write city there"
                @placechanged="getData"
                types="(cities)"
            >
            </vue-google-autocomplete>
        </v-card-text>
    </v-card>
</template>

<script>
import VueGoogleAutocomplete from 'vue-google-autocomplete'

export default {
    components: {
        VueGoogleAutocomplete
    },
    methods: {
        getData: function (data) {
            this.$emit('cityselected', data);
        }
    }
}
</script>

<style>

</style>