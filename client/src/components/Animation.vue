<template>
    <img 
        class='animation' 
        src='https://i.pinimg.com/originals/76/8d/41/768d41c38389731667cf6972ae5bdd1c.gif'
        :style="{left: this.$props.x - 50 + 'px', top: this.$props.y - 100 + 'px', width: '100px'}">
</template>

<script>

export default {
    name: 'Animation',
    props: ['x','y']
}
</script>

<style>
.animation {
    position: fixed
}
</style>