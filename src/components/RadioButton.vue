<template>
  <div :class="className">
    <label v-for="value in values">
      <input type="radio" :value='value' v-model="checked" @change="onCheck">
      <span></span>
      {{value}}
    </label>
  </div>
</template>

<script>
  export default {
    name: "RadioButton",
    props: {
      values: Array,
      model: String,
      className: String,
      initial: String,
    },
    data() {
      return {
        checked: '',
      }
    },
    beforeMount: function (){
      this.initial ? this.checked = this.initial : null;
    },
    methods: {
      onCheck() {
        this.$emit('change', {
          "checked": this.checked,
          "model": this.model
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  label {
    display: block;
    position: relative;
    padding-left: 25px;
    cursor: pointer;
    user-select: none;
    line-height: 1.5;
    &:hover {
      & > span {
        background: #eee;
      }
    }
    input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      &:checked {
        & ~ span {
          border-color: #F28022;
          &:after {
            display: block;
          }
        }
      }
    }
    span {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      left: 0;
      height: 15px;
      width: 15px;
      border-radius: 50%;
      border: 1px solid #acacb5;
      &:after {
        border-radius: 50%;
        content: "";
        position: absolute;
        display: none;
        left: 4px;
        top: 4px;
        width: 7px;
        height: 7px;
        background: #F28022;

      }
    }
  }
</style>
