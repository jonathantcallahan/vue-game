<template>
  <div id="app" @keydown='move' tabindex='0'>
    <Character :location-x='location.character.x' :location-y='location.character.y'></Character>
  </div>
</template>

<script>
import Character from './components/Character'

export default {
  name: 'app',
  components: {
    Character
  },
  data: function () {
    return {
      location: {
        character: {
          x: 10,
          y: 10
        }
      }
    }
  },
  methods: {
    move: function (e) {
      const {keyCode} = e
      if(keyCode == 37 && this.location.character.x > 0) {this.location.character.x -= 2}
      if(keyCode == 38 && this.location.character.y > 0) {this.location.character.y -= 2}
      if(keyCode == 39) {this.location.character.x += 2}
      if(keyCode == 40) {this.location.character.y += 2}
    }
  }
}
</script>

<style>
#app {
  width: 400px;
  height: 400px;
  padding: 0px;
  margin: 0px
}
</style>
