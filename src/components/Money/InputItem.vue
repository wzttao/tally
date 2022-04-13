<template>
  <div>
    <label class="inputItem">
      <span class="name">{{fieldName}}</span>
      <input type="text"
             :value="value"
             @input="onValueChaged($event.target.value)"
             :placeholder="placeholder">
    </label>
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';

@Component
export default class InputItem extends Vue {
  @Prop({default:''}) readonly value! : string;
  @Prop({required:true}) fieldName!:string;
  @Prop() placeholder?:string;

  onValueChaged(value: String) {
    this.$emit('update:value', value);
  }


}
</script>

<style lang="scss" scoped>
.inputItem {
  font-size: 14px;
  padding-left: 16px;
  display: flex;
  align-items: center;

  .name {
    padding-right: 16px;
  }

  input {
    height: 40px;
    flex-grow: 1;
    border: none;
    background: transparent;
    padding-right: 16px;
  }
}
</style>