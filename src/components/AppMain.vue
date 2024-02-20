<script>

import { store } from '../store';

import axios from 'axios';

export default {

    data() {
        return {
           
            searchedMedia:'',

            store,

            apiKey: store.apiKey,
        }
    },

    methods: {
        searchMedia() {
            axios.get('https://api.themoviedb.org/3/search/movie?api_key=' + this.apiKey + this.searchedMedia).then((response) => {
                store.movies = response.data.results
            })
        }
    },


}


</script>

<template>
    <nav>
        <div class="nav-container p-3">
            <div class="text-danger fs-1">
                BOOLFLIX
            </div>

            <div>
                <input type="text" v-model="searchedMedia">
                <button @click="searchMedia()">SEARCH</button>
            </div>
        </div>
    </nav>

    <main>
        <ul v-for="movie in store.movies">
            <li>Titolo {{ movie.title }}</li>

            <li>Titolo Originale {{ movie.original_title }}</li>

            <li>Lingua {{ movie.original_language }}</li>

            <li>Voto {{ movie.vote_average }}</li>
        </ul>
    </main>
</template>

<style lang="scss" scoped>
.nav-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: black;
}
</style>