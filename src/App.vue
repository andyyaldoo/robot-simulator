<template>
  <div id="app">
    <Board
      v-bind:x="x + 1"
      v-bind:y="maxY - y"
      v-bind:direction="direction"
      v-bind:placed="placed"
    />
    <Control
      v-on:place="place"
      v-on:move="move"
      v-on:left="left"
      v-on:right="right"
      v-on:report="report"
    />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Board from './components/Board.vue';
import Control from './components/Control.vue';
import Direction from './enum';

export default Vue.extend({
  name: 'app',
  components: {
    Board,
    Control,
  },
  methods: {
    place(x: number, y: number, direction: Direction) {
      this.x = x;
      this.y = y;
      this.direction = direction;
      this.placed = true;
    },
    report() {
      if (this.x !== 0 && this.y !== 0) {
        this.rep =  `The robot is at X:${this.x}, Y:${this.y}, facing ${this.direction.toLowerCase()}`;
      } else {
        this.rep = 'The robot is not placed yet';
      }
      alert(this.rep);
    },
    left() {
      if (!this.placed) {
        return
      }
      if (this.direction === Direction.EAST) {
        this.direction = Direction.NORTH;
      } else if (this.direction === Direction.NORTH) {
        this.direction = Direction.WEST;
      } else if (this.direction === Direction.WEST) {
        this.direction = Direction.SOUTH;
      } else if (this.direction === Direction.SOUTH) {
        this.direction = Direction.EAST;
      }
    },
    right() {
      if (!this.placed) {
        return
      }
      this.left(); this.left(); this.left();
    },
    move() {
      if (!this.placed) {
        return
      }
      if (this.direction === Direction.EAST && this.x < this.maxX - 1) {
          this.x += 1;
      } else if (this.direction === Direction.SOUTH && this.y > this.minY - 1) {
          this.y -= 1;
      } else if (this.direction === Direction.WEST && this.x > this.minX - 1) {
          this.x -= 1;
      } else if (this.direction === Direction.NORTH && this.y < this.maxY - 1) {
          this.y += 1;
      }
    },
  },
  data() {
    return {
      x: 0,
      y: 0,
      direction: Direction.NORTH,
      maxX: 5,
      maxY: 5,
      minX: 1,
      minY: 1,
      rep: '',
      placed: false,
    };
  },
});
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
  }

  %container {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
  }

  html, body {
    @extend %container;
  }

  #app {
    @extend %container;
    padding: 1em;
  }
</style>
