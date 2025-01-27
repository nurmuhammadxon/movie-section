<template>
    <Box>
        <p class="text-5xl uppercase">Barcha kinolar soni: {{ allMoviesCount }}</p>
        <p class="text-4xl uppercase">Ko'rilgan kinolar soni: {{ favouriteMoviesCount }}</p>
    </Box>
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

<style scoped></style>