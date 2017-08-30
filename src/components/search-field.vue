<template>
  <div class="test">
    <div class="wrapper">
      <input v-model.trim="searchterm" placeholder="movie title here"/>
      <button type="button" name="button" @click="submit(searchterm)" :disabled="suggestions && suggestions.length == 0">Submit</button>
      <ul>
        <li v-for="suggestion in suggestions">
          <a  v-on:click="setSuggestion(suggestion.name)">{{ suggestion.name }}</a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
// https://github.com/krisk/Fuse
  props: {
    moviePlots: Array,
    minChars: {
      default: 3,
      type: Number
    }
  },

  data: function(){

    // Why return?
    return {
      searchterm: '',
      terms: [],
      suggestions: []
    }
  },

  methods: {

    submit: function(searchterm){
      this.$emit('submit', this.searchterm );
      this.searchterm = '';
    },

    searchPlots( term ){
      if( term.length >= this.minChars ){
        var x = this.moviePlots.filter(function(movie){
          term = term.toLowerCase();
          return movie.name.toLowerCase().indexOf(term) >= 0;
        })
        console.log('movie', x);
        return x;
      }
    },

    setSuggestion( suggestion ){
      console.log('suggestion', suggestion)
      this.searchterm = suggestion;
    }

  },

  watch: {
    searchterm: function ( term ) {
      this.suggestions = this.searchPlots( term );
    }
  }

}
</script>

<style lang="scss">

</style>
