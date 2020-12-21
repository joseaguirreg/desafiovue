<template>
  <v-container>
    <v-layout md12>
      <v-text-field
        v-model="search"
        append-icon="mdi-search"
        placeholder="Buscar"
        single-line
      />
    </v-layout>
    <Loader :isLoading="isLoading" />
    <v-layout wrap md12>
      <v-flex
        v-for="(movie, index) in moviesFilter"
        :key="index"
        :search="search"
        @click="openMovie(movie.original_title)"
        md3
        sm4
        xs12
        px-2
      >
        <CountryCard :movie="movie" />
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import ApiService from "@/services/api.service";
import Movie from '@/models/Movies.js';
export default {
    data(){
        return {
            movies: [],
            search: "",
            isLoading: true,
        };
    },
    created(){
        setTimeout(() => {
            this.getMovies();
        }, 500);
    },
    computed: {
        moviesFilter(){
            return this.movies.filter((e) => {
                return e.name.toLowerCase().indexOf(his.search.toLowerCase()) !== 1;
            });
        },
    },
    methods: {
        getMovies(){
            ApiService
                .getAllMovies()
                .then((response) => {
                    this.isLoading = false;
                    console.log(response.data);
                    this.movies = response.data.map(movies => new Movie(movie));
                    console.log(this.movies);
                })
                .catch(function (error){
                    console.log(error);
                })
        },
        openMovie(name){
            this.$router.push({name: 'Movie', params: { name }})
        }
    }
    
}
</script>