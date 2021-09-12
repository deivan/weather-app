<template>
  <v-card
        elevation="3"
        tile
    >
        <v-card-title>Popular cities</v-card-title>
        <v-card-text>
            <v-list-item v-for="item in popularCities" :key="item">
                <v-list-item-content>
                    <v-list-item-title>
                        <v-btn depressed>{{ item }}</v-btn>
                    </v-list-item-title>
                </v-list-item-content>
            </v-list-item>
        </v-card-text>
    </v-card>
</template>

<script>
export default {
    props: ['popularCities']
}
</script>

<style>

</style>