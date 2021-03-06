<template>
  <div class="mue-header">
    <div class="mue-header-left">
      <a class="mue-header-back" v-show="leftOptions.showBack" :transition="transition"
         @click.prevent.stop="onClickBack">{{leftOptions.backText}}</a>
      <div class="left-arrow" @click="onClickBack" v-show="leftOptions.showBack" :transition="transition"></div>
      <slot name="left"></slot>
    </div>
    <h1 class="mue-header-title" @click="$emit('on-click-title')">
      <span v-show="title" :transition="transition">{{title}}</span>
      <slot></slot>
    </h1>
    <div class="mue-header-right">
      <a class="mue-header-more" @click.prevent.stop="$emit('on-click-more')" v-if="rightOptions.showMore"></a>
      <slot name="right"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      leftOptions: {
        type: Object,
        default () {
          return {
            showBack: true,
            backText: 'Back',
            preventGoBack: false
          }
        }
      },
      title: String,
      transition: String,
      rightOptions: {
        type: Object,
        default () {
          return {
            showMore: false
          }
        }
      }
    },
    methods: {
      onClickBack () {
        if (this.leftOptions.preventGoBack) {
          this.$emit('on-click-back')
        } else {
          window.history.back()
        }
      }
    }
  }
</script>

<style lang="less">
  @import '../../styles/variable.less';

  .mue-header {
    position: relative;
    padding: 3px 0;
    box-sizing: border-box;
    background-color: @header-background-color;
  }

  .mue-header .mue-header-title, .mue-header h1 {
    margin: 0 88px;
    margin-left: 100px;
    line-height: 40px;
    text-align: center;
    height: 40px;
    font-size: 18px;
    font-weight: 400;
    width: auto;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    color: @header-title-color;
  }

  .mue-header .mue-header-title > span {
    display: inline-block;
  }

  .mue-header .mue-header-left, .mue-header .mue-header-right {
    position: absolute;
    top: 14px;
    display: block;
    font-size: 14px;
    line-height: 21px;
    color: @header-text-color;
  }

  .mue-header .mue-header-left a, .mue-header .mue-header-left button, .mue-header .mue-header-right a, .mue-header .mue-header-right button {
    float: left;
    margin-right: 8px;
    color: @header-text-color;
  }

  .mue-header .mue-header-left a:active, .mue-header .mue-header-left button:active, .mue-header .mue-header-right a:active, .mue-header .mue-header-right button:active {
    opacity: .5
  }

  .mue-header .mue-header-left {
    left: 18px
  }

  .mue-header .mue-header-left .mue-header-back {
    padding-left: 16px
  }

  .mue-header .mue-header-left .left-arrow {
    position: absolute;
    width: 30px;
    height: 30px;
    top: -5px;
    left: -5px;

    &
    :before {
      content: "";
      position: absolute;
      width: 12px;
      height: 12px;
      border: 1px solid @header-arrow-color;
      border-width: 1px 0 0 1px;
      transform: rotate(315deg);
      top: 8px;
      left: 7px;
    }
  }

  .mue-header .mue-header-left .left-arrow:before {
    content: "";
    position: absolute;
    width: 12px;
    height: 12px;
    border: 1px solid @header-arrow-color;
    border-width: 1px 0 0 1px;
    transform: rotate(315deg);
    top: 8px;
    left: 7px;
  }
  .mue-header .mue-header-right {
    right: 15px
  }

  .mue-header .mue-header-right a, .mue-header .mue-header-right button {
    margin-left: 8px;
    margin-right: 0
  }

  .mue-header .mue-header-right .mue-header-more:after {
    content: "\2022\0020\2022\0020\2022\0020";
    font-size: 16px;
  }

  .mue-header-fade-in-right-enter {
    animation: fadeinR .5s;
  }

  .mue-header-fade-in-left-enter {
    animation: fadeinL .5s;
  }

  @keyframes fadeinR {
    0% {
      opacity: 0;
      transform: translateX(80px);
    }
    100% {
      opacity: 1;
      transform: translateX(0);
    }
  }

  @keyframes fadeinL {
    0% {
      opacity: 0;
      transform: translateX(-80px);
    }
    100% {
      opacity: 1;
      transform: translateX(0);
    }
  }
</style>
