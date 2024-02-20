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
                console.log(response.data);
                store.movie = response.data
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
</template>

<style lang="scss" scoped>
.nav-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: black;
}
</style>