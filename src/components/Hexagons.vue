<template lang="pug">
  #hexagons_wrapper(:class="{ hidden: hideAll }")
    .animator-fade(:class="{ 'animated': animated }")
    #center.hexagon(ref='centerHexagon', @click="animateHexagons", :class="{ 'fade-out': animated }")
    #click-indicator(:class="{ hide: animated }") Click me
    template(v-for="y in yAxisCount")
      .hexagon(v-for="x in xAxisCount", :style="cordinates(x, y)") {{ y }}
</template>

<script>
export default {
  data () {
    return {
      animated: false,
      hideAll: false
    }
  },
  computed: {
    width () {
      let center = this.$refs.centerHexagon
      return center ? center.clientWidth : 104
    },
    height () {
      let center = this.$refs.centerHexagon
      return center ? center.clientHeight : 120
    },
    windowWidth () {
      return window.innerWidth
    },
    windowHeight () {
      return window.innerHeight
    },
    xAxisCount () {
      let result = Math.ceil(this.windowWidth / this.width) + 1

      if (result % 2 === 0) {
        result += 1
      }

      return result
    },
    yAxisCount () {
      let result = Math.ceil(this.windowHeight / (this.height * 0.75)) + 1

      if (result % 2 === 0) {
        result += 1
      }

      return result
    }
  },
  mounted () {
    // window.console.log(this.$refs.centerHexagon.clientHeight)
  },
  methods: {
    cordinates (x, y) {
      let margin = 3

      let centerX = Math.ceil(this.xAxisCount / 2)
      let centerY = Math.ceil(this.yAxisCount / 2)

      let outerHeight = this.height + margin * 2
      let outerWidth = this.width + margin * 2

      let top = (y - centerY) * (outerHeight * 0.75)
      let left = (x - centerX) * outerWidth

      if (y % 2 !== centerY % 2) {
        left -= outerWidth / 2
      }

      return {
        top: top + 'px',
        left: left + 'px'
      }
    },
    animateHexagons () {
      let self = this

      self.animated = true

      setTimeout(function () {
        // self.animated = false
        self.$emit('done', true)
        self.hideAll = true
      }, 3000)
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/variables.scss';

  $hexagon-width: 104px;
  $hexagon-height: 120px;

  #hexagons_wrapper {
    position: relative;
    display: inline-block;
    font-size: 0;
  }

  .hexagon {
    display: inline-block;
    margin: 3px;
    position: absolute;
    z-index: 3;
    background-color: $bg-color;
    clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0 25%);
    color: white;
    width: $hexagon-width;
    height: $hexagon-height;

    &#center {
      cursor: pointer;
      position: relative;
      z-index: 4;
      background-color: $primary;
      transition: all 1s;

      &.fade-out {
        background-color: $bg-color;
      }
    }
  }

  #click-indicator {
    display: inline-block;
    border: 1px solid white;
    background-color: $bg-color;
    color: white;
    padding: 6px 10px;
    border-radius: 10px;
    position: fixed;
    top: calc(50% + 80px);
    left: 50%;
    transform: translateX(-50%);
    z-index: 5;
    font-size: 12px;
    transition: all .5s;

    &.hide {
      opacity: 0;
      pointer-events: none;
    }

    &:before, &:after {
      content: '';
      display: inline-block;
      border-bottom: 10px solid transparent;
      border-right: 10px solid transparent;
      border-left: 10px solid transparent;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
    }

    &:before {
      border-bottom-color: white;
      top: -10px;
    }

    &:after {
      border-bottom-color: $bg-color;
      top: -8px;
    }
  }

  @keyframes glowing {
    0%   {
      opacity: 0;
    }
    50%  {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  .glowing {
    animation-name: glowing;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    animation-timing-function: ease-out;
  }

  @keyframes expand {
    0%   {
      width: $hexagon-width;
      height: $hexagon-height;
    }
    100% {
      width: 2080px;
      height: 2400px;
    }
  }

  .animator {
    z-index: 1;

    &:before, &:after {
      top: 50%;
      left: 50%;
      position: absolute;
      content: '';
      display: inline-block;
      clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0 25%);
      width: $hexagon-width;
      height: $hexagon-height;
      background-color: $primary;
      transform: translateX(-50%) translateY(-50%);
      animation-duration: 3s;
      // animation-iteration-count: infinite;
      animation-timing-function: ease-in-out;
    }

    &:before {
      background-color: $primary;
    }

    &:after {
      background-color: $bg-color;
      animation-delay: .15s;
    }

    &.animated {
      &:before, &:after {
        animation-name: expand;
      }
    }
  }

  @keyframes expand-fade {
    0%   {
      width: 100px;
      height: 100px;
    }
    100% {
      width: 2500px;
      height: 2500px;
    }
  }

  .animator-fade {
    z-index: 1;

    &:before {
      top: 50%;
      left: 50%;
      position: absolute;
      content: '';
      display: inline-block;
      width: $hexagon-width;
      height: $hexagon-height;
      clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0 25%);
      background: radial-gradient($bg-color 50%, $primary 70%, $bg-color);
      transform: translateX(-50%) translateY(-50%);
      animation-duration: 3s;
      // animation-iteration-count: infinite;
      animation-timing-function: ease-in-out;
    }

    &.animated {
      &:before {
        animation-name: expand-fade;
      }
    }
  }
</style>
