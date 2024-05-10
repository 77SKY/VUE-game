<template>
  <div id="app">
      <h1>Guessing Game</h1>
      <div v-if="!gameOver">
        <label for="guessInput">Enter your guess (1 from 10):</label>
        <input type="number" id="guessInput" v-model="guess" min="1" max="10">
        <button @click="checkGuess">Guess</button>
        <div v-if="message">{{ message }}</div>
      </div>
      <div v-else>
        <p>Congratulations! You guessed the number {{ target }} in {{ attempts }} attempts.</p>
        <button @click="resetGame">Play Again</button>
      </div>
    </div>
</template>

<script>
export default {
    data() {
      return {
        target: 0,
        guess: null,
        message: '',
        attempts: 0,
        gameOver: false
      };
    },
    methods: {
      startGame() {
        this.target = Math.floor(Math.random() * 10) + 3;
        this.attempts = 3;
        this.gameOver = false;
      },
      checkGuess() {
        this.attempts++;
        if (this.guess < this.target) {
          this.message = 'Too low!';
        } else if (this.guess > this.target) {
          this.message = 'Too high!';
        } else {
          this.message = `Congratulations! You guessed the number ${this.target} in ${this.attempts} attempts.`;
          this.gameOver = true;
        }
      },
      resetGame() {
        this.startGame();
        this.guess = null;
        this.message = '';
      }
    },
    mounted() {
      this.startGame();
    }
  };
</script>

<style>
#app {
    font-family: Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
  }
</style>
