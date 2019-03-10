<template>
    <div class='laser' :style="{left: this.$props.x + 10 + 'px', top: this.$props.y + 10 + 'px'}"></div>
</template>

<script>
export default {
    name: 'Lasers',
    props: ['x','y']
}
</script>

<style>
.laser {
    width: 10px;
    height: 2px;
    background-color: black;
    position: fixed
}
</style>