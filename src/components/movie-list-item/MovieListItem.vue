<template>
    <li class="flex justify-between list-group-item "
        v-bind:class="[{ like: movie.like }, { favourite: movie.favourite }]">
        <span @click="$emit('onToggle', { id: movie.id, prop: 'like' })" class="list-group-item-lebal">{{ movie.name
            }}</span>
        <input type="number" class="list-group-input" v-bind:value="movie.viewers">
        <div class=" flex justify-center items-center">
            <button @click="$emit('onToggle', { id: movie.id, prop: 'favourite' })" type="button" class="btn-cookie">
                <i class='bx bxs-cookie'></i>
            </button>

            <button @click="$emit('onRemove', movie.id)" type="button" class="btn-trash">
                <i class='bx bxs-trash'></i>
            </button>

            <i class="bx bxs-star"></i>
        </div>
    </li>
</template>

<script>
export default {
    props: {
        movie: {
            type: Object,
            required: true,
        },
    },
    methods: {
        onLikeClick() {
            this.$emit('onLike', this.movie.id)
        },
        onFavouriteClick() {
            this.$emit('onFavourite', this.movie.id)
        }
    }
}
</script>

<style scoped>
.list-group-item {
    width: 100%;
    border-bottom: 1px solid #3d5a80;
    padding: 15px 20px;
}

.list-group-item:last-child {
    border-bottom: none;
}

.list-group-item span {
    line-height: 35px;
    font-size: 20px;
    cursor: pointer;
    width: 550px;
}

.list-group-item input {
    line-height: 35px;
    font-size: 20px;
    text-align: center;
    outline: none;
}

.list-group-item button {
    width: 35px;
    height: 35px;
    margin: 3px;
    font-size: 17px;
    border: none;
    cursor: pointer;
}

.list-group-item .btn-cookie {
    color: #e09f3e;
}

.list-group-item .btn-trash {
    color: #e5383b;
}

.list-group-item .bxs-star {
    width: 35px;
    height: 35px;
    text-align: center;
    line-height: 35px;
    font-size: 16px;
    color: #ffd700;
    transition: 0.3s all;
    transform: translateX(30px);
    opacity: 0;
}

.list-group-item.like .bxs-star {
    opacity: 1;
    transform: translateX(0);
}

.list-group-item.favourite .list-group-item-lebal,
.list-group-item.favourite .list-group-input {
    color: #e09f3e;
}
</style>