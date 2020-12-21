<template>
    <v-card class="mb-5">
    <v-img
        class="white--text"
        height = "200px"
        :src='movie.poster_path'
    >
        <v-card-title>{{ movie.original_title }}</v-card-title>
    </v-img>
        <v-card-text>
            <div class="subtititle-1"> {{movie.vote_count}}</div>
        </v-card-text>
        </v-card>
</template>

<script>
import Movie from '@/models/Movie.js'
export default {
    props:{
        movie:{
            type: Object,
            requred: true,
            default: new Movie()
        },
    },
    methods: {

    },
};
</script>

<style>

</style>