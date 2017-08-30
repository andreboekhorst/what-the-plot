<template>
  <div>
    <h1>{{ score }} / {{ currentQuestionIndex }} | {{ maxQuestions }}</h1>
    <plotview :plotString="currentMovie.plot"></plotview>
    <searchfield @submit="onsubmit" :moviePlots="plotArr"></searchfield>
  </div>
</template>

<script>

import plotview from './components/plotview.vue';
import searchfield from './components/search-field.vue';
import autosuggest from './components/autosuggest.vue';
import movieList from './assets/plots.json';

export default {

  name: 'app',

  data () {
    return {
      currentMovie: {},
      plotArr: [],
      maxQuestions: 20,
      currentQuestionIndex: 0,
      score: 0,
      timer: 20000,
    }
  },

  components: {
    'plotview': plotview,
    'searchfield': searchfield,
    'autosuggest': autosuggest
  },

  methods: {

    getRandomMovie: function(){
      return this.plotArr[Math.floor(Math.random()* this.plotArr.length)];
    },

    addScore: function(){
        this.score++;
    },

    nextQuestion: function(){
      this.currentQuestionIndex++;
      this.currentMovie = this.getRandomMovie();
    },

    onMistake: function(){
      console.log('it was', this.currentMovie.name );
    },

    onsubmit: function( val ){

      if( this.checkAnswer(val) ){
        console.log('correct');
        this.addScore();
      } else {
        this.onMistake();
      }

      this.nextQuestion();

    },

    checkAnswer( answer ){
      return this.currentMovie.name == answer;
    }

  },

  watch: {

   currentQuestionIndex: function ( index ) {
     if( index > this.maxQuestions ){
       console.log('maxing out')
     }
   },

  },

  created: function(){
    this.plotArr = movieList;
    this.nextQuestion();
  }

}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
