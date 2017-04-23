<template>
  <div>
    <h1>{{ score }}</h1>
    <plotview :plotString="currentMovie.plot"></plotview>
    <searchfield @submit="onsubmit"></searchfield>
    <p v-for="plot in plotArr">{{ plot.id }}</p>
  </div>
</template>

<script>

import plotview from './components/plotview.vue';
import searchfield from './components/search-field.vue';

export default {

  name: 'app',

  data () {
    return {
      currentMovie: {},
      plotArr: [],
      maxQuestions: 20,
      currentQuestionIndex: 1,
      score: 0,
      timer: 20000, // Get more points if fast?
    }
  },

  components: {
    'plotview': plotview,
    'searchfield': searchfield,
  },

  methods: {

    getRandomMovie: function(){
      return this.plotArr[Math.floor(Math.random()* this.plotArr.length)];
    },

    showplot: function(){
      this.currentMovie = this.getRandomMovie();
    },

    addScore: function(){
        this.score++;
    },

    nextQuestion: function(){

    },

    onsubmit: function( val ){

      if( this.checkAnswer(val) ){
        console.log('correct');
        this.addScore();
      } else {
        console.log('wrong');
      }

      this.nextQuestion();

    },

    checkAnswer( answer ){
      return this.currentMovie.id == answer;
    }

  },
  created: function(){

    this.$http.get('/src/assets/plots.json').then(response => {
      this.plotArr = JSON.parse(response.bodyText);
      this.showplot();
    }, response => {
      // error callback
    });

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
