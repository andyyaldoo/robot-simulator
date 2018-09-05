<template>
<main id="board">
  <div class="grid" id="boxes">
    <div>(0, 4)</div>
    <div>(1, 4)</div>
    <div>(2, 4)</div>
    <div>(3, 4)</div>
    <div>(4, 4)</div>

    <div>(0, 3)</div>
    <div>(1, 3)</div>
    <div>(2, 3)</div>
    <div>(3, 3)</div>
    <div>(4, 3)</div>

    <div>(0, 2)</div>
    <div>(1, 2)</div>
    <div>(2, 2)</div>
    <div>(3, 2)</div>
    <div>(4, 2)</div>

    <div>(0, 1)</div>
    <div>(1, 1)</div>
    <div>(2, 1)</div>
    <div>(3, 1)</div>
    <div>(4, 1)</div>

    <div>(0, 0)</div>
    <div>(1, 0)</div>
    <div>(2, 0)</div>
    <div>(3, 0)</div>
    <div>(4, 0)</div>
  </div>
  <div class="grid" id="robots">
    <div id="robot" v-show="shouldShow" v-bind:style="{gridColumnStart: x, gridRowStart: y}" v-bind:class="[direction.toLowerCase()]"></div>
  </div>
</main>
</template>

<script lang="ts">
import Vue from 'vue';
import Direction from '../enum';
export default Vue.extend({
  name: 'board',
  props: {
    x: Number,
    y: Number,
    direction: String,
    placed: Boolean,
  },
  computed: {
    shouldShow: {
      get(): boolean {
        return this.placed;
      },
    },
  },
});
</script>


<style lang="scss" scoped>
  main {
      width: 45vw;
      height: 45vw;
      position: relative;
      border: 12px solid #235;
      border-radius: 10%;
      background: url("https://images.unsplash.com/photo-1520588882256-7084d04976a5?ixlib=rb-0.3.5&s=61f1d04d8431405f6a7d561b51f5584e&auto=format&fit=crop&w=2251&q=80") center center no-repeat

  }
  #boxes {
    width: 100%;
    height: 100%;
    text-align: center;
    position: absolute;
    top: 0;
    left: 0;
    display: grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-rows: repeat(5, 20%);
  }

  #robots {
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
    display: grid;
    grid-template-columns: repeat(5, 20%);
    grid-template-rows: repeat(5, 20%);
  }

  #robot {
    border-radius: 50%;
    grid-row-end: span 1;
    grid-column-end: span 1;
    background: red;
    position: relative;

    &::after {
      position: absolute;

      content: '>';

      width: 20px;
      height: 20px;

      // To make it center (with fixed height)
      text-align: center;
      margin: auto;
      left: 0; top: 0; right: 0; bottom: 0;
    }

    &.south::after {
        transform: rotate(90deg)
    }

    &.west::after {
      transform: rotate(180deg)
    }

    &.north::after {
      transform: rotate(-90deg)
    }
  }
</style>
