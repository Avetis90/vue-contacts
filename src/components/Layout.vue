<template>
    <div class="layout">
        <Header/>
        <div class="container py-5">
            <slot>

            </slot>
        </div>
        <Footer/>
    </div>

</template>

<script>
    import Header from './Header';
    import Footer from './Footer';

    export default {
        name: "Layout",
        components: {Header, Footer}
    }
</script>

<style>
    .layout {
        min-height: 100vh;
        height: 100%;
        width: 100%;
        display: flex;
        flex-direction: column;
    }
</style>
