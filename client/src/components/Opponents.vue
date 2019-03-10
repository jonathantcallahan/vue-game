<template>
    <div class='opponent' :style="{left: this.$props.x + 'px', top: this.$props.y + 'px'}">
        <img :style="{display: this.$props.animation ? 'block' : 'none'}" src='https://i.pinimg.com/originals/76/8d/41/768d41c38389731667cf6972ae5bdd1c.gif'>
    </div>
</template>

<script>
export default {
    name: 'Opponents',
    props: ['x','y','animation']
}
</script>

<style>
.opponent {
    position: fixed;
    width: 10px;
    height: 10px;
    border: 2px solid black
}
</style>