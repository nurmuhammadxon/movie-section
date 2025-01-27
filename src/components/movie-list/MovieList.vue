<template>
    <ul class="movie-list">
        <MovieListItem v-for="movie in movies" v-bind:movie="movie" />
    </ul>
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

<style scoped>
.movie-list {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgb(0, 0, 0, 0.15);
}
</style>