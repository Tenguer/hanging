<template>
  <div id="pendu">
    <img src="../assets/img/one-piece-logo.png" alt="One Piece" height="100">

    <h1>Find the ONE PIECE</h1>
    <p>
      <span v-for="(val , i) in word_to_guess">
        <span v-if="foundLetters.indexOf(i) === -1">_ </span>
        <span v-else>{{ word_to_guess[i] }}</span>
      </span>
    </p>
    <form class="box" @submit.prevent="tryLetter">
        <input type="text" class="try" maxlength="1" v-model="letter_of_user">
        <input type="submit">
    </form>

    <div v-show="won">You won</div>
    <p>
      <button @click="init">Restart</button>
    </p>
    <div class="hangman_img" :class="hangman_class"></div>
  </div>
</template>

<script>
  export default {
    name: 'pendu',
    data () {
      return {
        points: null,
        words: ['Zoro', 'Raftel', 'Nami', 'Luffy', 'Chopper', 'Ussopp', 'Law', 'Franky', 'Jinbe', 'Sanji'],
        word_to_guess: '',
        letter_of_user: '',
        foundLetters: [],
        won: false
      }
    },
    created () {
      this.init()
    },
    computed: {
      hangman_class () {
        return 'step-' + (10 - this.points + 1)
      }
    },
    methods: {
      init () {
        var random = Math.floor(Math.random() * this.words.length)
        this.word_to_guess = this.words[random]
        this.points = 10
        this.foundLetters = []
        this.won = false
      },
      tryLetter () {
        var found = this.testLetterInWord(this.letter_of_user, this.word_to_guess)

        if (found === false) {
          if (this.points === 0) {
            alert('End Game')
          } else {
            alert('Try Another Letter')
          }
        } else {
          this.foundLetters = this.foundLetters.concat(found)

          if (this.foundLetters.length === this.word_to_guess.length) {
            this.won = true
          }
        }
        this.letter_of_user = ''
      },
      testLetterInWord (letter, word) {
        if (this.points === 0) {
          return false
        }

        word = word.toLowerCase()
        letter = letter.toLowerCase()

        var indexOfLetter = word.indexOf(letter)

        if (this.foundLetters.indexOf(indexOfLetter) > -1) {
          this.points -= 1
          return false
        }

        var foundLetters = []

        for (var i = 0; i < word.length; i++) {
          if (letter === word[i]) {
            foundLetters.push(i)
          }
        }
        if (foundLetters.length === 0) {
          this.points -= 1
          return false
        } else {
          return foundLetters
        }
      }
    }
  }
</script>

<style scoped>
  #pendu {
    font-family: arial, sans-serif;
    text-align: center;
  }

  h1 {
    margin: 20px 0;
    font-size: 48px;
    background: ;
  }

  p {
    margin: 10px 0;
    font-size: 36px;
  }

  .chance {
    width: 100%;
    height: 50px;
    font-size: 20px;
  }

  .box {
    display: flex;
    justify-content: space-around;
    margin: 20px 0;
  }

  input {
    display: block;
    width: 50%;
    margin: 0;
    font-size: 36px;
  }

  .hangman_img {
    height: 92px;
    margin: 10px auto;
    background: transparent url(../assets/img/sprite.png);
    transform: scale(3,3);
    transform-origin: 50% 0;
  }

  .step-1 {
    width: 56px;
    background-position: -106px 0;
  }
  .step-2 {
    width: 56px;
    background-position: -0 -256px;
  }
  .step-3 {
    width: 55px;
    background-position: -62px -261px;
  }
  .step-4 {
    width: 38px;
    background-position: -65px -61px;
  }
  .step-5 {
    width: 63px;
    background-position: -208px -61px;
  }
  .step-6 {
    width: 83px;
    background-position: -363px -61px;
  }
  .step-7 {
    width: 59px;
    background-position: -523px -153px;
  }
  .step-8 {
    width: 54px;
    background-position: -132px -256px;
  }
  .step-9 {
    width: 68px;
    background-position:-196px -256px;
  }
  .step-10{
    width: 86px;
    background-position: -262px -256px;
  }
</style>
