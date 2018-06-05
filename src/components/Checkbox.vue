<template>
  <label :class="className">
    <input ref="checkbox" v-model="checked" type="checkbox" @change="onCheck">
    <span class="checkmark" :style='style'></span>
    {{value}}
  </label>
</template>

<script>
  export default {
    name: "Checkbox",
    data() {
      return{
        checked: false
      }
  },
    props: [
      'value',
      'model',
      'className',
      'backgroundColor'
    ],
    computed:{
      style() {
       return this.backgroundColor ?
         `background: ${this.backgroundColor}; border: none`
         : null;
      }
    },
    methods: {
      onCheck() {
        this.$emit('change', {
          "value": this.$props.value,
          "checked" : this.checked,
          "model" : this.$props.model
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  label{
    display: block;
    position: relative;
    padding-left: 20px;
    cursor: pointer;
    user-select: none;
    &:hover{
      .checkmark{
        background-color: #eee;
      }
    }
    input{
      position: absolute;
      opacity: 0;
      cursor: pointer;
      &:checked{
        & ~ .checkmark{
          border-color: #F28022;
          &:after{
            display: block;
          }
        }
      }
    }
    .checkmark{
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      left: 0;
      height: 15px;
      width: 15px;
      border-radius: 2px;
      border: 1px solid #acacb5;
      background-color: transparent;
      &:after{
        content: "";
        position: absolute;
        display: none;
        left: 4px;
        bottom: 2px;
        width: 5px;
        height: 13px;
        border: solid #F28022;
        border-width: 0 2px 2px 0;
        transform: rotate(45deg)
      }
    }
  }
</style>
