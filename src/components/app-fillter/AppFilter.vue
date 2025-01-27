<template>
    <div class="app-fillter">
        <button class="border-[1px] border-black p-[5px] transition duration-150"
            :class="filterName === 'all' ? 'bg-black text-white' : 'bg-white text-black'"
            @click="filterHandler('all')">Barcha
            kinolar</button>
        <button class="border-[1px] border-black p-[5px] transition duration-150"
            :class="filterName === 'popular' ? 'bg-black text-white' : 'bg-white text-black'"
            @click="filterHandler('popular')">Mashhur
            kinolar</button>
        <button class="border-[1px] border-black p-[5px] transition duration-150"
            :class="filterName === 'mostViewers' ? 'bg-black text-white' : 'bg-white text-black'"
            @click="filterHandler('mostViewers')">Eng
            ko'p ko'rilgan kinolar</button>
    </div>
</template>

<script>
export default {
    props: {
        updateFilterHandler: {
            type: Function,
            required: true,
        },
        filterName: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            filter: 'all',
        }
    },
    methods: {
        filterHandler(filter) {
            this.filter = filter
            this.updateFilterHandler(this.filter)
        }
    },
}
</script>

<style scoped>
.app-fillter {
    border: 1px solid #000;
    display: inline-block;
    border-radius: 4px;
}
</style>