<template>
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form flex mt-[1rem]">
            <input type="text"
                class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200 bg-white new-movie-label"
                placeholder="Qanday kino?">
            <input type="text"
                class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200 bg-white new-movie-label"
                placeholder="Nechi marotaba ko'rilgan?">
            <button
                class="box-border border border-black rounded-md p-[4px] ml-[5px] hover:bg-black hover:text-white bg-white"
                type="submit">Qo'shish</button>
        </form>
    </div>
</template>

<script>
export default {
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