<script>

import { store } from '../store';

import axios from 'axios';

export default {

    data() {
        return {

        }
    },

    methods: {
        searchContent() {
            axios.get('...').then((response) => {
                console.log(response.data)
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
                <input type="text">
                <button @click="searchContent()">SEARCH</button>
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