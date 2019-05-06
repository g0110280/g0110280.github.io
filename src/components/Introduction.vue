<template lang="pug">
  #content_wrapper(:class="{ hide: !showWelcome }")
    img#logo(src="@/assets/logo.png", :class="{ show: welcomeFinished }")
    #welcome.typing_wrapper(:class="{ show: !welcomeFinished }")
      h1 I'm Stream, welcome!
    ul#navbar(:class="{ show: welcomeFinished }")
      li: a(href="#") Gallery
      li: a(href="#") Blogs
      li: a(href="#") Github
</template>

<script>
  export default {
    data () {
      return {
        showWelcome: false,
        welcomeFinished: false
      }
    },
    mounted () {
      // this.play()
    },
    methods: {
      play () {
        this.showWelcome = true

        setTimeout(() => {
          this.welcomeFinished = true
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
      animation-iteration-count: 5;
      animation-fill-mode: forwards;
    }
  }

  ul#navbar {
    display: flex;
    justify-content: space-between;
    list-style: none;
    padding: 0;
    opacity: 0;
    transition: all 1s;
    transition-delay: .7s;
    margin-top: -50px;

    &.show {
      margin-top: 50px;
      opacity: 1;
    }

    li {
      position: relative;

      + * {
        margin-left: 80px;
      }

      &:before, &:after {
        color: $primary;
        opacity: 0;
        padding: 0 20px;
        transition: all .3s;
        font-size: 30px;
        display: inline-block;
      }

      &:before {
        content: '{';
        transform: translateX(20px);
      }

      &:after {
        content: '}';
        transform: translateX(-20px);
      }

      &:hover {
        cursor: pointer;

        &:before, &:after {
          opacity: 1;
          transform: translateX(0);
        }
      }

      @keyframes expand-underline {
        0% {
          width: 0;
        }

        100% {
          width: 100%;
        }
      }

      a {
        font-size: 24px;
        font-weight: 300;
        color: white;
        text-decoration: none;
        display: inline-flex;
        align-items: center;
        display: inline-block;

        &:after {
          content: '';
          display: block;
          margin: 10px auto;
          width: 0;
          height: 2px;
          background: white;
          transition: all .3s;
        }
      }

      &:hover {
        a {
          &:before, &:after {
            background: $bg-color;
          }
        }
      }
    }

    &.show {
      a {
        &:before, &:after {
          animation-name: expand-underline;
          animation-duration: .5s;
          animation-delay: 2s;
          animation-fill-mode: forwards;
        }
      }
    }
  }

  #logo {
    opacity: 0;
    transition: all 1s;
    transition-delay: .7s;
    width: 200px;

    &.show {
      opacity: 1;
    }
  }

  #welcome {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    opacity: 0;

    &.show {
      opacity: 1;
    }
  }
</style>
