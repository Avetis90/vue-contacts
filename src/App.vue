<template>
    <div id="app">
        <layout>
            <Home />
        </layout>
    </div>
</template>

<script>
    import Layout from './components/Layout.vue'
    import Home from './pages/Home';


    export default {
        name: 'App',
        components: {Home, Layout}
    }
</script>

<style>
    @import "~bootstrap/dist/css/bootstrap.min.css";

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }
    .is-invalid .multiselect__tags{
        border-color: #dc3545;
    }
</style>
