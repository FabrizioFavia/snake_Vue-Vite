<script>
export default {
  name: 'mainPart',
  components: {

  },
  data() {
    return {

      greetings: 'ciao',
      currentSquare: [1, 2, 3],
      up: 38,
      down: 40,
      left: 37,
      right: 39,
      leftBorder: [1, 21, 31, 41, 51, 61, 71, 81, 91],
      rightBorder: [10, 20, 30, 40, 50, 60, 70, 80, 90, 100],
      topBorder: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20],
      bottomBorder: [91, 92, 93, 94, 95, 96, 97, 98, 99, 100],
      apple: /* Math.floor(Math.random(1) * 100) */7,
      points: 0,
      
    }
  },
  mounted() {
    document.addEventListener("keydown", this.move);
  },
  beforeUnmount() {
    document.removeEventListener("keydown", this.move);
  },
  methods: {
    
    move(event, index, curva, curvaDue) {
      if (this.currentSquare.includes(this.apple)) {
        this.currentSquare.unshift((this.apple) - this.currentSquare.length)
        this.apple = Math.floor(Math.random() * 100);
        this.points += 1
      } else {
        if (event.keyCode === this.down && this.bottomBorder.includes(this.currentSquare)) {
          
          this.currentSquare -= 380;
        } else if (event.keyCode === this.down) {
          this.currentSquare = this.currentSquare.map(e => e + 1)
        } else if (event.keyCode === this.up && this.topBorder.includes(this.currentSquare)) {
          this.currentSquare += 380;
        } else if (event.keyCode === this.up && this.currentSquare > 20) {
          this.currentSquare -= 20;
        } else if (event.keyCode === this.left && this.leftBorder.includes(this.currentSquare[0])) {
          this.currentSquare = this.currentSquare.map(e => e + 9)
        } else if (event.keyCode === this.left) {
          this.currentSquare = this.currentSquare.map(e => e - 1)


        } else if (event.keyCode === this.right && this.rightBorder.includes(this.currentSquare[this.currentSquare.length - 1])) {
          this.currentSquare = this.currentSquare.map(e => e - 9)
        } else if (event.keyCode === this.right) {
          
          this.currentSquare = this.currentSquare.map(e => e + 1)
          console.log(this.currentSquare);


        }
      }
      return this.currentSquare;
    }
  }
}



</script>

<template>
  <div class="points text-white">POINTS: {{ points }}</div>
  <div class="gameSquare d-flex flex-wrap">
    <template v-for="(n, index) in 100">
      <div :class="currentSquare.includes(n) ? 'green' : n == apple ? 'red' : ''" @keydown="move(event, index)"
        class="square">{{ n }}</div>
    </template>
  </div>
</template>

<style lang="scss" scoped>
@use '../style.scss' as *;

button {
  background-color: red;
}
</style>