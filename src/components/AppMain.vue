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
        // AXIOS GET METHOD
        searchMedia() {
            axios.get('https://api.themoviedb.org/3/search/movie?api_key=' + this.apiKey + this.searchedMedia).then((response) => {
                store.movies = response.data.results
            })
        },


        langFlag(flag) {

            if (flag == 'it') {

                return "fi fi-it";

            } else if (flag == 'en') {

                return "fi fi-gb"

            }

        }



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
                <button @click="searchMedia()">SEARCH</button>
            </div>
        </div>
    </nav>

    <main>
        <ul v-for="movie in store.movies">
            <li>Titolo: {{ movie.title }}</li>

            <li>Titolo: Originale {{ movie.original_title }}</li>

            <li>
                Lingua: <span :class="langFlag(movie.original_language)"></span>
            </li>

            <li>Voto: {{ movie.vote_average }}</li>
        </ul>
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

// <span class="fi fi-"></span>

</style>