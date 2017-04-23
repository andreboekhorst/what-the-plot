<template>
  <div class="test">
    <input v-model="searchterm"/>
    <button type="button" name="button" @click="onSubmit(searchterm)">lala</button>
    <hr />
    <ul>
      <li v-for="term in terms">{{ term }}</li>
    </ul>
  </div>
</template>

<script>
export default {

  data: function(){
    return {
      searchterm: 'default',
      terms: []
    }
  },
  methods: {

    onSubmit: function(searchterm){
      this.terms.push(searchterm);
      this.searchterm = ""
      console.log(this.terms)
    }

  }

}
</script>

<style lang="scss">

</style>
