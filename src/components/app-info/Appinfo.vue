<template>
    <div class="app-info">
        <p class="text-5xl uppercase">Barcha kinolar soni: {{ allMoviesCount }}</p>
        <p class="text-4xl uppercase">Ko'rilgan kinolar soni: {{ favouriteMoviesCount }}</p>
    </div>
</template>

<script>
export default {
    props: {
        allMoviesCount: {
            type: Number,
            required: true,
        },
        favouriteMoviesCount: {
            type: Number,
            required: true,
        }
    },
}
</script>

<style scoped>
.app-info {
    padding: 1.5rem;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgb(0, 0, 0, 0.15);
}
</style>