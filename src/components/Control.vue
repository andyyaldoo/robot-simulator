<template>
    <div id="controls">
        <div class="control">
            <label for="x">X:</label>
            <input type="number" name="x" id="x" v-model="x">
            <label for="y">Y:</label>
            <input type="number" name="y" id="y" v-model="y">
            <select v-model="direction">
                <option v-bind:key="dir" v-for="dir in directions">
                    {{ dir }}
                </option>
            </select>
        </div>
        <div class="control">
            <button id="place" @click="$emit('place', parseInt(x), parseInt(y), direction)">Place</button>
        </div>
        <div class="control">
            <button id="move" @click="$emit('move')">Move</button>
        </div>
        <div class="control">
            <button id="left" @click="$emit('left')">Left</button>
        </div>
        <div class="control">
            <button id="right" @click="$emit('right')">Right</button>
        </div>
        <div class="control">
            <button id="report" @click="$emit('report')">Report</button>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Direction from '../enum';
export default Vue.extend({
    name: 'controls',
    data() {
       return {
           x: 0,
           y: 0,
           direction: Direction.NORTH,
           directions: Object.values(Direction),
           placed: false,
       };
    },
});
</script>

<style lang="scss" scoped>
  #controls {
    height: 45vw;
    width: 45vw;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;

    #x, #y {
        width: 3em;
    }

    .control {
        button {
            height: 4em;
            width: 8em;
            outline: none;
        }
    }
  }
</style>
