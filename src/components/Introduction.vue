<template lang="pug">
  #content_wrapper(:class="{ hide: !showWelcome }")
    .typing_wrapper
      h1 I'm Stream, welcome!
    ul#navbar(:class="{ show: showNav }")
      li: a(href="#") Works
      li: a(href="#") Blogs
      li: a(href="#") Github
</template>

<script>
  export default {
    data () {
      return {
        showWelcome: false,
        showNav: false
      }
    },
    mounted () {
      //
    },
    methods: {
      play () {
        this.showWelcome = true

        setTimeout(() => {
          this.showNav = true
        }, 5000)
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import '@/assets/scss/variables.scss';

  #content_wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  @keyframes typing {
    0%   {
      width: 0;
      color: $primary;
    }
    100% {
      width: 100%;
      color: $primary;
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

  .typing {
    width: 10px;
    color: transparent;
    overflow: hidden;
    white-space: nowrap;
    display: inline-block;
    animation-name: typing;
    animation-duration: .5s;
    animation-timing-function: linear;
    animation-fill-mode: forwards;
    position: relative;

    &:after {
      position: absolute;
      right: 0;
      margin-left: 20px;
      content: '';
      display: inline-block;
      background-color: $primary;
      width: 10px;
      height: 100%;
      animation-name: glowing;
      animation-duration: 1s;
      animation-iteration-count: infinite;
      animation-iteration-count: 4;
      animation-fill-mode: forwards;
    }
  }

  h1 {
    height: 40px;
    animation-delay: 2s;
    margin: 0;
  }

  h2 {
    /*opacity: 0;*/
    animation-delay: 4s;
  }

  .typing_wrapper {
    display: inline-block;
    position: relative;
    white-space: nowrap;
    text-align: center;
    transition: all 1s;

    &.shifted {
      margin-bottom: 30px;
    }

    > * {
      width: 10px;
      color: transparent;
      overflow: hidden;
      white-space: nowrap;
      display: inline-block;
      animation-name: typing;
      animation-duration: 1s;
      animation-timing-function: linear;
      animation-fill-mode: forwards;
      position: relative;
    }

    &:after {
      /*position: absolute;
      top: 0;
      right: 0;*/
      /*margin-left: 20px;*/
      content: '';
      display: inline-block;
      background-color: $primary;
      width: 10px;
      height: 30px;
      animation-name: glowing;
      animation-duration: 1s;
      /*animation-iteration-count: infinite;*/
      animation-iteration-count: 4;
      animation-fill-mode: forwards;
    }
  }

  ul#navbar {
    display: flex;
    justify-content: space-between;
    width: 400px;
    list-style: none;
    padding: 0;
    opacity: 0;
    transition: all 1s;
    margin-top: -50px;

    &.show {
      margin-top: 50px;
      opacity: 1;
    }

    li a {
      font-size: 24px;
      font-weight: 300;
      color: white;
      text-decoration: none;
    }
  }
</style>
