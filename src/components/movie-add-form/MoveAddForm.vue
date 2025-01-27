<template>
    <Box>
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form flex mt-[1rem]" v-on:submit.prevent="addMovies">
            <input type="text"
                class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200 bg-white new-movie-label"
                placeholder="Qanday kino?" v-model="name" v-on:input="name = $event.target.value">
            <input type="text"
                class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200 bg-white new-movie-label"
                placeholder="Nechi marotaba ko'rilgan?" v-model="viewers" v-on:input="viewers = $event.target.value">
            <PrimaryButton type="submit">Qo'shish</PrimaryButton>
        </form>
    </Box>
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
    },
}
</script>

<style></style>