<template>
  <button class="button" @click="$emit('click',$emit)">
    <slot/>
  </button>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component
export default class Button extends Vue {

}
</script>

<style lang="scss" scoped>
.button {
  height: 40px;
  color: #ffffff;
  background: #767676;
  border: none;
  border-radius: 5px;
  padding: 0 14px;

  &-wrapper {
    text-align: center;
    padding: 5px;
    margin-bottom: 5px;
  }
}
</style>