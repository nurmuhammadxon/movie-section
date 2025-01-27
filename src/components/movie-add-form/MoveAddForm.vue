<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form flex mt-[1rem]" v-on:submit.prevent="addMovies">
            <input type="text"
                class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200 bg-white new-movie-label"
                placeholder="Qanday kino?" v-model="name" v-on:input="name = $event.target.value">
            <input type="text"
                class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200 bg-white new-movie-label"
                placeholder="Nechi marotaba ko'rilgan?" v-model="viewers" v-on:input="viewers = $event.target.value">
            <button
                class="box-border border border-black rounded-md p-[4px] ml-[5px] hover:bg-black hover:text-white bg-white"
                type="submit">Qo'shish</button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: "",
            viewers: "",
        }
    },
    methods: {
        addMovies() {
            if (!this.name && !this.viewers || isNaN(Number(this.viewers))) {
                this.name = ''
                this.viewers = ''
                return
            }
            const newMovie = {
                name: this.name,
                viewers: Number(this.viewers),
                favourite: false,
                like: false,
            }
            this.$emit('creatMovie', newMovie)
            this.name = ''
            this.viewers = ''
        }
    }
}
</script>

<style>
.movie-add-form {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgb(0, 0, 0, 0.15);
}
</style>