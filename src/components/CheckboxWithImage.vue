<template>
  <label :style="style" :class="{ orange:checked }">
    <input ref="checkbox" v-model="checked" type="checkbox" @change="onCheck">
    <img v-if="icon" class="checkmark" :src="srcComp">
    {{value}}
  </label>
</template>

<script>


  export default {
    name: "Checkbox",
    data() {
      return {
        checked: false
      }
    },
    props: [
      'value',
      'model',
      'icon'
    ],
    computed: {
      srcComp() {
        return `./static/assets/cp-${this.icon}.png`;
      },
      style(){
        return this.icon ? null: "padding: 10px 4px 4px 4px";
      }
    },
    methods: {
      onCheck() {
        this.$emit('change', {
          "value": this.$props.value,
          "checked": this.checked,
          "model": this.$props.model
        })
      }
    }
  }
</script>

<style lang="scss" scoped>
  label {
    display: block;
    position: relative;
    padding: 4px 4px 7px 4px;
    cursor: pointer;
    user-select: none;
    border: 1px solid #999999;
    border-radius: 3px;
    &.orange {
      color: #f46f13;
      border-color: #f46f13;
      &:hover{
        border-color: #f46f13
      }
    }
    &:hover {
      border-color: #ad9585;
      & > .checkmark {
        filter: grayscale(80%);
      }
    }

    input {
      position: absolute;
      opacity: 0;
      cursor: pointer;
      &:checked {
        color: #f46f13;
        & ~ .checkmark {
          filter: sepia(15%);
        }
      }
    }
    .checkmark {
      position: relative;
      display: inline;
      transform: translateY(4px) scaleX(-1);
      left: 0;
      height: 20px;
      filter: grayscale(100%);
      opacity: 0.8;
    }
  }
</style>
