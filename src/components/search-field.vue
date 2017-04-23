<template>
  <div class="test">
    <input v-model.trim="searchterm" placeholder="movie title here"/>
    <button type="button" name="button" @click="submit(searchterm)">lala</button>
  </div>
</template>

<script>
export default {
  props: {

  },
  data: function(){
    return {
      searchterm: '',
      terms: []
    }
  },
  methods: {

    submit: function(searchterm){
      this.$emit('submit', this.searchterm );
    }

  }

}
</script>

<style lang="scss">

</style>
