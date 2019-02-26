<template>
    <div class="backgroundImage"/>
</template>

<script>
    export default {
        name: 'BackgroundImage',
    };
</script>

<style lang="scss" scoped>
    .backgroundImage {
        position: fixed;
        width: 100%;
        height: 100vh;
        top: 0;
        z-index: -1;
        background-image: url('../assets/background.jpg');
        background-repeat: no-repeat;
        background-size: cover; 
        background-position: 30% 0%;
    }
    .backgroundImage::after {
            content: '';
            background: rgba(0,0,0,.3);
            position: absolute;
            top: 0;
            left: 0;
            z-index: 1;
            width: 100%;
            height: 100vh;
    }

</style>
