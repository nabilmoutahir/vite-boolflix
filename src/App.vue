<script>
    import AppHeader from './components/AppHeader.vue'

    import { store } from './store';

    export default {
        data() {
            return {
                store,

            }
        },

        components: { AppHeader }


    }

    

</script>

<template>
  
    <AppHeader></AppHeader>

</template>

<style lang="scss">

    @use './styles/general.scss' ;

</style>
