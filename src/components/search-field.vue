<template>
  <div class="test">
    <input v-model.trim="searchterm"/>
    <button type="button" name="button" @click="submit(searchterm)">lala</button>
    <hr />
    <ul>
      <li v-for="term in terms">{{ term }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {

  },
  data: function(){
    return {
      searchterm: 'default',
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
