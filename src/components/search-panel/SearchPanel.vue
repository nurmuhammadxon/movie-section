<template>
    <input type="text"
        class="w-full border border-gray-300 rounded-md p-2 focus:outline focus:outline-sky-200  focus:bg-white search-input "
        placeholder="Kinolarni qidirish" v-model="term" @input="changeHandler">
</template>

<script>
export default {
    props: {
        updateTermHandler: {
            type: Function,
            required: true,
        },
    },
    data() {
        return {
            term: ''
        }
    },
    methods: {
        changeHandler(e) {
            this.term = e.target.value
            this.updateTermHandler(this.term)
        }
    },
}
</script>

<style scoped>
.search-input {
    margin-top: 2rem;
    margin-bottom: 1rem;
    padding: 1.5rem;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgb(0, 0, 0, 0.15);
}
</style>