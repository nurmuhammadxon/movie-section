<template>
    <div class="box">
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "Box",
}
</script>

<style>
.box {
    margin-top: 2rem;
    padding: 1.5rem;
    background-color: #fcfaf5;
    border-radius: 4px;
    box-shadow: 15px 15px 15px rgb(0, 0, 0, 0.15);
}
</style>