<template>
    <div>
        <PrimaryButton class="border-[1px] border-black p-[5px] transition duration-150" v-for="btn in filterButtons"
            :key="btn.name" :class="filterName === btn.name ? 'bg-black text-white' : 'bg-white text-black'"
            @click="filterHandler(btn.name)">
            {{ btn.title }}
        </PrimaryButton>
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
            filterButtons: [
                {
                    title: "Barcha kinolar",
                    name: "all",
                },
                {
                    title: "Mashhur kinolar",
                    name: "popular",
                },
                {
                    title: "Eng ko'p ko'rilgan kinolar",
                    name: "mostViewers",
                },
            ],
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

<style scoped></style>