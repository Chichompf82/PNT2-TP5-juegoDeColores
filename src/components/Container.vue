<template lang="html">

  <section class="container">
    <Square
      v-for="(color, key) of colors"
      :key="key"
      :color="color"
      :ClickSquare="ClickSquare"
    />
  </section>

</template>

<script lang="js">
  import Square from "./Square.vue";
  export default  {
    
    components: {
      Square
    },
    name: 'game-container',
    props: ['colors', 'ClickSquare'],
    mounted () {

    },
    data () {
      return {

      }
    },
    methods: {

    },
    computed: {
      
    }
}


</script>

<style scoped lang="css">
.container {
  margin: 20px auto;
  max-width: 600px;
}
</style>
