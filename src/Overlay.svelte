<script>
    export let zIndex = 10;
</script>

<div class="overlay" style="z-index: {zIndex}" />

<style>
    .overlay {
        position: fixed;
        left: 0;
        top: 0;
        width: 100vw;
        height: 100vh;
        background-color: black;
        opacity: 0.9;
    }
</style>
