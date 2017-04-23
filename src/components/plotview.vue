<template>
  <div class="plot">
    <p>{{ plotString }}</p>
  </div>
</template>

<script>
export default {
  props: {
    plotString: String
  }

}
</script>

<style lang="scss">
  .plot{
    font-size: 20px;
  }
</style>
