<template>
    <div id="app">
        <div class="container">
            <mainPage/>
        </div>
    </div>
</template>

<script>
import mainPage from "./components/mainPage";

export default {
    name: 'App',
    components: {
        mainPage,
    },
    data() {
        return {

        }
    },
    methods: {

    },
    mounted() {

    }
}
</script>
<style lang="scss">
@media (max-width: 1360px) {
    .container {
        width: 100%;
    }
}
@media (max-width: 992px) {

}
</style>
