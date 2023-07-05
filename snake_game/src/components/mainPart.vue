<script>
export default {
  name: 'mainPart',
  components: {

  },
  data() {
    return {

      greetings: 'ciao',
      snake: [1, 2, 3],
      up: 38,
      down: 40,
      left: 37,
      right: 39,
      leftBorder: [1, 21, 31, 41, 51, 61, 71, 81, 91],
      rightBorder: [10, 20, 30, 40, 50, 60, 70, 80, 90, 100],
      topBorder: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
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

    moveSnake(position, i) {

      if (i >= 0) {
        const current = this.snake[i - 1];
        this.snake[i - 1] = position;
        this.moveSnake(current, (i - 1));
      }
    },

    move(event, index) {
      if (this.snake.includes(this.apple)) {
        this.snake.unshift((this.apple) - this.snake.length)
        this.apple = Math.floor(Math.random() * 100);
        this.points += 1
      } else {
        const position = this.snake[this.snake.length - 1];
        if (event.keyCode === this.down && this.bottomBorder.includes(this.snake[this.snake.length-1])) {
          this.snake[this.snake.length - 1] -= 90;
        } else if (event.keyCode === this.up && this.topBorder.includes(this.snake[this.snake.length-1])) {
          this.snake[this.snake.length-1]+=90;
        }   else if (event.keyCode === this.right && this.rightBorder.includes(this.snake[this.snake.length-1])) {
          this.snake[this.snake.length-1]-=9;
        }else if (event.keyCode === this.left && this.leftBorder.includes(this.snake[this.snake.length-1])) {
          this.snake[this.snake.length-1]+=9;
          
        } else if (event.keyCode === this.right) {
          this.snake[this.snake.length - 1] += 1;
        }else if (event.keyCode === this.left) {
          this.snake[this.snake.length - 1] -= 1;
        }else if (event.keyCode === this.up) {
          this.snake[this.snake.length - 1] -= 10;
        }else if (event.keyCode === this.down) {
          this.snake[this.snake.length - 1] += 10;
        }
        this.moveSnake(position, (this.snake.length - 1));
      } 
      console.log(this.snake);
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