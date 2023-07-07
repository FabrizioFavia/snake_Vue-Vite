<script>
export default {
  name: 'mainPart',
  components: {

  },
  data() {
    return {
      snake: [1, 2, 3],
      up: 38,
      down: 40,
      left: 37,
      right: 39,
      leftBorder: [1, 21, 31, 41, 51, 61, 71, 81, 91],
      rightBorder: [10, 20, 30, 40, 50, 60, 70, 80, 90, 100],
      topBorder: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
      bottomBorder: [91, 92, 93, 94, 95, 96, 97, 98, 99, 100],
      movements: [],
      toCheck: false,
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

    moveSnake(position, i) {

      if (i >= 0) {
        const current = this.snake[i - 1];
        this.snake[i - 1] = position;
        this.moveSnake(current, (i - 1));
      }
    },
    checkIfArrayIsUnique(array) {
      let head = array[array.length-1]
      for (let i = array.length-2; i >= 0; i--) {
        const element = array[i];

        if (element = head) {
          this.toCheck = true
          return true
        } 
      }
        return this.toCheck;
    },

    move(event, index) {

      let freeMove = false;

      if (this.snake.includes(this.apple)) {
        this.snake.unshift('x')
        this.apple = Math.floor(Math.random() * 100);
        this.points += 1
      } else {
        const position = this.snake[this.snake.length - 1];
        if (event.keyCode === this.down && this.bottomBorder.includes(this.snake[this.snake.length - 1])) {
          this.snake[this.snake.length - 1] -= 90;
        } else if (event.keyCode === this.up && this.topBorder.includes(this.snake[this.snake.length - 1])) {
          this.snake[this.snake.length - 1] += 90;
        } else if (event.keyCode === this.right && this.rightBorder.includes(this.snake[this.snake.length - 1])) {
          this.snake[this.snake.length - 1] -= 9;
        } else if (event.keyCode === this.left && this.leftBorder.includes(this.snake[this.snake.length - 1])) {
          this.snake[this.snake.length - 1] += 9;

        } else if (event.keyCode === this.right && this.movements[this.movements.length - 1] !== 'l') {
          freeMove = true
          this.movements.push('r');
          console.log(this.movements);
          this.snake[this.snake.length - 1] += 1;

        } else if (event.keyCode === this.left && this.movements[this.movements.length - 1] !== 'r') {
          freeMove = true
          this.movements.push('l');
          console.log(this.movements);
          this.snake[this.snake.length - 1] -= 1;
        } else if (event.keyCode === this.up && this.movements[this.movements.length - 1] !== 'd') {
          freeMove = true
          this.movements.push('u');
          this.snake[this.snake.length - 1] -= 10;
        } else if (event.keyCode === this.down && this.movements[this.movements.length - 1] !== 'u') {
          freeMove = true
          this.movements.push('d');
          this.snake[this.snake.length - 1] += 10;
        }
        if (freeMove==true) {
          this.moveSnake(position, (this.snake.length - 1));
        }
        /* if (this.toCheck == true) {
          alert('hai perso');
        } */
      }
      return this.snake;
    }
  }
}



</script>

<template>
  <div class="points text-white">POINTS: {{ points }}</div>
  <div class="gameSquare d-flex flex-wrap">
    <template v-for="(n, index) in 100">
      <div :class="snake.includes(n) ? 'green' : n == apple ? 'red' : ''" @keydown="move(event, index)" class="square">{{
        n }}</div>
    </template>
  </div>
</template>

<style lang="scss" scoped>
@use '../style.scss' as *;

button {
  background-color: red;
}
</style>