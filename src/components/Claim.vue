<template>
    <div class="claimWrapper">
        <h1 class="claim">SPACER</h1>
        <p class="subclaim">Begin your journey through our amazing galazy.</p>
        <p class="subclaim">Type anything space-related to start.</p>
    </div>
</template>

<script>  
export default {
    name: 'Claim',
}
</script>

<style lang="scss" scoped>
    .claimWrapper{
        color: rgb(175, 255, 208);
        display: flex;
        text-align: center;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .claim {
        font-size: 4rem;
        margin: 0;
    }
    
    .subclaim {
        font-size: 1rem;
        margin: 2rem 0 0 0;
    }
</style>
