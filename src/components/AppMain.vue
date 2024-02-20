<script>
// IMPORTS
import { store } from '../store';

import axios from 'axios';

export default {

    data() {
        return {

            searchedMedia: '',

            store,

            apiKey: store.apiKey,
        }
    },

    methods: {
        // SEARCH ALL MEDIAS
        searchAllMedia() {
            this.searchMedia();
            this.searchMediaTv();
        },

        // AXIOS GET MOVIE METHOD
        searchMedia() {
            axios.get('https://api.themoviedb.org/3/search/movie?api_key=' + this.apiKey + this.searchedMedia).then((response) => {
                store.movies = response.data.results
            })
        },

        // AXIOS GET TV
        searchMediaTv() {
            axios.get('https://api.themoviedb.org/3/search/tv?api_key=' + this.apiKey + this.searchedMedia).then((response) => {
                store.tvs = response.data.results
                console.log(response.data.results)
            })
        },

        // FLAGS
        langFlag(flag) {

            if (flag == 'it') {

                return "fi fi-it";

            };
            
            if (flag == 'en') {

                return "fi fi-gb"

            };

        },

    },


}


</script>

<!-- TEMPLATE -->
<template>
    <nav>
        <div class="nav-container p-3">
            <div class="text-danger fs-1">
                BOOLFLIX 
            </div>

            <div>
                <input type="text" v-model="searchedMedia">
                <button @click="searchAllMedia()">SEARCH</button>
            </div>
        </div>
    </nav>

    <main>
        <!-- MOVIES -->
        <div>
            <h2>Movies</h2>
            <!-- V-FOR -->
            <ul v-for="movie in store.movies">
                <li>Titolo: {{ movie.title }}</li>

                <li>Titolo Originale: {{ movie.original_title }}</li>

                <li>
                    Lingua: <span :class="langFlag(movie.original_language)"></span>
                </li>

                <li>
                    Voto:
                <i v-for="star in 5" :class="star <= Math.ceil(movie.vote_average / 2) ? 'fa-solid fa-star' : 'fa-regular fa-star'" class="text-warning"></i>
                </li>

                <li>Poster:
                    <div>
                        <img :src="'https://image.tmdb.org/t/p/w342/' + movie.poster_path" alt="">
                    </div>
                </li>
            </ul>
        </div>

        <!-- TV SHOWS -->
        <div>
            <h2>Tv Shows</h2>
            <!-- V-FOR -->
            <ul v-for="tv in store.tvs">
                <li>Titolo: {{ tv.name }}</li>

                <li>Titolo Originale: {{ tv.original_name }}</li>

                <li>
                    Lingua: <span :class="langFlag(tv.original_language)"></span>
                </li>

                <li>Voto: {{ Math.ceil(tv.vote_average / 2) }}</li>

                <li>Poster:
                    <div>
                        <img :src="'https://image.tmdb.org/t/p/w342/' + tv.poster_path" alt="">
                    </div>
                </li>
            </ul>
        </div>

    </main>
</template>

<!-- STYLE -->
<style lang="scss" scoped>
    .nav-container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        background-color: black;
    }

</style>