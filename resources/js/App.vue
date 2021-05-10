<template>
        <navbar />
        <router-view :key="store.state.language" />
     
 
</template>

<script>

import store from './store/index.js'
import navbar from "./components/navbar.vue";
import { provide } from 'vue';
export default {
    components: { navbar },
    setup(){
        provide('store',store)
        return { store }
    }
};
</script>
<style>

</style>
