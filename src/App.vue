<template lang="pug">
  #app
    hexagons(@done="$refs.intro.play()")

    introduction(ref="intro")
</template>

<script>
import Hexagons from '@/components/Hexagons'
import Introduction from '@/components/Introduction'

export default {
  components: { Hexagons, Introduction },
  data () {
    return {
      //
    }
  },
  methods: {
    //
  }
}
</script>

<style lang="scss">
  @import '@/assets/scss/variables.scss';

  * {
    font-family: 'Open Sans', sans-serif;
  }

  #app {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: $bg-color;
    color: $primary;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .text-center {
    text-align: center;
  }

  .hidden {
    display: none !important;
  }
</style>
