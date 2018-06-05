<template>
    <div @click="closeModal" class="modal">
      <div ref="content" :class="{content, visible:content.isModalOpen}">
        <span @click="closeModal" class="close-button">
          <font-awesome-icon :icon="times"></font-awesome-icon>
        </span>
        {{contentJSON}}
      </div>
    </div>
</template>

<script>
  import FontAwesomeIcon from "@fortawesome/vue-fontawesome";
  import { faTimes } from "@fortawesome/fontawesome-free-solid";

  export default {
    name: "Modal",
    components: {
      FontAwesomeIcon
    },
    props: {
      content: Object,
      modalHandler: Function
    },
    data (){
      return {

      }
    },
    methods: {
      closeModal(event){
        event.stopPropagation();
        if (event.target === this.$refs.content){
          return
        }
        this.$emit('close')
      }
    },
    computed: {
      contentJSON(){
        return  JSON.stringify(this.content.formData)
      },
      times(){
        return faTimes
      },
    },

  }
</script>

<style lang="scss" scoped>
  .modal{
    width: 100%;
    height: 100%;
    position: fixed;
    background-color: rgba(0,0,0,0.4);
    z-index: 1;
    top: 0;
    left: 0;
    .content{
      position: relative;
      top: -100%;
      left: 50%;
      transform: translate(-50%, -50%);
      text-align: center;
      border-radius: 10px;
      background: #fff;
      width: 80%;
      padding: 25px;
      user-select: none;
      z-index: 2;
      animation-name: slidetop;
      animation-duration: 0.5s;
      @keyframes slidetop {
        from {top: -100%; opacity: 0}
        to { top: 50%; opacity: 1}
      }
      &.visible{
        top: 50%;
      }
      .close-button{
        position: absolute;
        top: 10px;
        right: 10px;
        color: #aeaeae;
        cursor: pointer;
        &:hover{
          color: #777;
        }
      }
    }
  }

</style>
