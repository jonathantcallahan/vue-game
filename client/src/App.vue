<template>
  <div id="app" @keydown='move' tabindex='0'>
    <div class='score-container'>
      <div>Lives: {{this.lives}}</div>
      <div>Score: {{this.score}}</div>
      <div>Accuray: {{Math.round((this.accuracy.plus/(this.accuracy.plus + this.accuracy.minus)) * 100, 2)}}%</div>
    </div>
    <Character :location-x='location.character.x' :location-y='location.character.y'></Character>
    <Lasers v-for='(laser,i ) in location.lasers' :x='laser.x' :key="i + '-laser'" :y='laser.y'></Lasers>
    <Opponents v-for='(opponent, i) in location.opponents' :key="i + '-opponent'" :x='opponent.x' :y='opponent.y'></Opponents>
    <Animations v-for='(animation, i) in location.animations' :key="i + '-animation'" :x='animation.x' :y='animation.y'></Animations>
  </div>
</template>

<script>
import Character from './components/Character'
import Lasers from './components/Lasers'
import Opponents from './components/Opponents'
import Animations from './components/Animation'

export default {
  name: 'app',
  components: {
    Character,
    Lasers,
    Opponents,
    Animations
  },
  data: function () {
    return {
      location: {
        character: {
          x: 10,
          y: 10
        },
        lasers: [],
        opponents: [],
        animations: []
      },
      score: 0,
      lives: 5,
      game: true,
      accuracy: {
        plus: 0,
        minus: 0
      }
    }
  },
  methods: {
    move: function (e) {
      const {keyCode} = e
      if(keyCode == 37 && this.location.character.x > 0) {this.location.character.x -= 15}
      if(keyCode == 38 && this.location.character.y > 0) {this.location.character.y -= 15}
      if(keyCode == 39) {this.location.character.x += 15}
      if(keyCode == 40) {this.location.character.y += 15}
      //console.log(keyCode)
      if(keyCode == 32) {this.location.lasers.push({x:this.location.character.x, y:this.location.character.y})}
      if(keyCode == 219) {this.game = !this.game}
    },
    moveLasers: function () {
      this.game && this.location.lasers.forEach((laser,i) => {
        laser.x += 10
        this.location.lasers[i] = laser
        if(laser.x > 1000) { 
          this.location.lasers.splice(i,1)
          this.accuracy.minus++
        }
        this.location.opponents.forEach((opponent, f) => {
          if(Math.abs(opponent.x - laser.x) < 15 && Math.abs(opponent.y - laser.y) < 15 ) {
            this.location.lasers.splice(i,1)
            this.location.opponents.splice(f,1)
            this.location.animations.push({...opponent})
            const animationIndex = this.location.animations.length - 1
            const removeAnimation = () => {
              this.location.animations.splice(animationIndex,1)
            }
            this.accuracy.plus ++
            setTimeout(removeAnimation,1200)
            this.score += 10
          }
        })
      })
      setTimeout(this.moveLasers,100)
    },
    moveOpponents: function () {
      this.game && this.location.opponents.forEach((opponent,i) => {
        opponent.x -= 10
        this.location.opponents[i] = opponent
        if(opponent.x < 0) {
          this.location.opponents.splice(i,1)
          this.lives -= 1
          if(this.lives == 0) { this.game = false }
        }
      })
      setTimeout(this.moveOpponents, 100)
    },
    createOpponents: function () {
      this.game && this.location.opponents.push({x:1000, y:Math.floor(Math.random() * 800)})
      setTimeout(this.createOpponents, 5000)
    }
  },
  mounted: function () {
    this.moveLasers()
    this.createOpponents()
    this.moveOpponents()
  }
}
</script>

<style>
#app {
  width: 80vw;
  height: 80vh;
  padding: 0px;
  margin: 0px
}

#app:focus {
  outline: none
}

.score-container {
  position: fixed;
  top: 20px;
  right: 20px
}
</style>
