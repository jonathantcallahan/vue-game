<template>
    <div class='character-container' >
        <div v-bind:style="{top:this.$props.locationY + 'px', left: this.$props.locationX + 'px'}" class='character'></div>
    </div>
</template>

<script>
export default {
    name: 'Character',
    props: ['location-x', 'location-y']
}
</script>

<style>
.character {
    width: 10px;
    height: 10px;
    background-color: black;
    position: relative
}
</style>