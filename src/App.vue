<template>
  <div id="app">
    <h1 class="title">Rock, Paper, Scissors!</h1>
    <div class="flex-row buttons">
      <button class="flex-item" 
      v-for="choice in playerChoices"
      :key="choice.id" 
      @click="selectChoice(choice)"
      :disabled="playerChoice"
      
      >
      <img :src='choice.image' >
      <h4>{{choice.label}}</h4>
      </button>
    </div>
    <div class="winner-circle flex-row" v-if="winner !==''">
     <div class="flex-item">
      <h4>Player Chose: </h4>
      <img :src='playerChoice.image' />
     </div>
     <div>
        <h4 class="winner">{{winner}}</h4>
      <button @click="resetGame">Reset Game</button>
     </div>
        <div class="flex-item">
      <h4>Computer Chose: </h4>
      <img :src='compChoice.image' />
     </div>
    </div>
    <div class="scoreboard">
     
        <div class="score">Player Score</div>
        <div class="score">Computer Score</div>
        <div class="score">Draws</div>
        <div class="score">{{playerScore}}</div>
        <div class="score">{{compScore}}</div>
        <div class="score">{{tie}}</div>
      
    </div>
  </div>
</template>

<script>
import choices from './choices';
export default {
  name: 'App',
  components: {},
  data: () => ({
    playerChoices: choices,
    playerChoice: null,
    compChoice: null, 
    winner: '',
    playerScore: 0,
    compScore: 0,
    tie: 0
  }),
  methods: {
    selectChoice(value){
      this.playerChoice = value
      this.compChoice = this.playerChoices[Math.floor(Math.random()* choices.length)]
      this.checkWinner()
    },
    checkWinner(){
      if(this.playerChoice.id === 1 && this.compChoice.id === 1){
        this.winner = `It's a draw!`
        this.tie++
      }
      if(this.playerChoice.id === 1 && this.compChoice.id === 2){
        this.winner = `Computer Won!`
        this.compScore++
      }
      if(this.playerChoice.id === 1 && this.compChoice.id === 3){
        this.winner = `Player Won!`
        this.playerScore++ 
      }
      if(this.playerChoice.id === 2 && this.compChoice.id === 1){
        this.winner = `Player Won!`
      }
      if(this.playerChoice.id === 2 && this.compChoice.id === 2){
        this.winner = `It's a draw!`
        this.tie++
      }
      if(this.playerChoice.id === 2 && this.compChoice.id === 3){
        this.winner = `Computer Won!`
        this.compScore++
      }
      if(this.playerChoice.id === 3 && this.compChoice.id === 1){
        this.winner = `Computer Won!`
        this.compScore++
      }
      if(this.playerChoice.id === 3 && this.compChoice.id === 2){
        this.winner = `Player Won!`
        this.playerScore++
      }
      if(this.playerChoice.id === 3 && this.compChoice.id === 3){
        this.winner = `It's a draw!`
        this.tie++
      }
    },
    resetGame(){
      this.winner = ''
      this.playerChoice = null
      this.compChoice = null
    }
  }
}
</script>

<style>
html {
  background-color: #16b5c7;
  /* background-image: url('https://i.imgur.com/werzdNG.png'); */
  background-repeat: no-repeat;
  background-size: cover;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
  color: #f4f6f9;
}

.flex-row {
  padding: 1em;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.flex-item {
  margin: 15px;
  padding: 1em;
  max-height: 12em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  background-color: #303030;
  border-radius: 4px;
  border: 1px solid rgba(255, 255, 255, 0);
  color: #f4f6f9;
}

button {
  border: 0;
  cursor: pointer;
  transition: all 0.3s ease;
}

button:disabled {
  cursor: not-allowed;
}

button:hover:not(:disabled) {
  /* opacity: 0.8; */
  border: 1px solid rgba(255, 255, 255, 0.4);
}

.flex-item img {
  width: 250px;
  max-height: 8em;
  align-content: center;
  object-fit: contain;
}

.winner-circle {
  margin-top: 2em;
  border: 1px solid rgba(255, 255, 255, 0.2);
  padding: 1em;
  border-radius: 4px;
}

.winner-circle button {
  padding: 1em 2em;
  border-radius: 4px;
  border: 0;
  background-color: rgb(0, 0, 0);
  font-weight: 700;
  color: white;
  box-shadow: rgba(0, 0, 0, 0.26)
              0px 10px 36px 0px;
  
}

.winner-circle button:hover {
  border: 0;
}

.winner {
  background-color: rgb(247, 255, 2);
  padding: 1em .5em;
  border-radius: 4px;
  border: 0;
  font-weight: 700;
  box-shadow: rgba(0, 0, 0, 0.26)
              0px 10px 36px 0px;
  color: black
  
}

.title{
  color: yellow;
 text-shadow: 2px 3px 5px #000000;
}

.score{
  margin: 10px;
}
.scoreboard{
  background-color: rgb(253, 253, 49);
  color: black;
  font-size: 1.25em;
  font-weight: 700;
  margin-top: 20px;
  margin-left: 25%;
  margin-right: 25%;
  border: solid black 3px;
  display:grid;
  grid-template-columns: repeat(3, 0.5fr);
  grid-template-rows: repeat(2, 0.5fr);
  grid-column-gap: 3px;
  grid-row-gap: 10px;
  box-shadow: rgba(0, 0, 0, 0.26)
              0px 10px 36px 0px;
  
}



</style>
