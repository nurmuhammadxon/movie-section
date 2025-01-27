<template>
    <Box>
        <ul>
            <MovieListItem v-for="movie in movies" :movie="movie" :key="movie.id" @onToggle="$emit('onToggle', $event)"
                @onRemove="$emit('onRemove', $event)" />
        </ul>
    </Box>
</template>

<script>
import MovieListItem from '../movie-list-item/MovieListItem.vue'
export default {
    components: {
        MovieListItem,
    },
    props: {
        movies: {
            type: Array,
            required: true,
        },
    },
}
</script>

<style scoped></style>