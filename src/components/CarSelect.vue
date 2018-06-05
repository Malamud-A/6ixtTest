<template>
  <div class="container">
    <div v-for="(_,index) in dataJSON.makes" class="car-select">
      <div class="make-select-container">
        <span>Marke</span>
        <div class="make-select">
          <font-awesome-icon class="faChevron" :icon="chevron"></font-awesome-icon>
          <select name="tst1" id="1" v-model="dataJSON.makes[index]">
            <option v-for="(_,key) in cars">{{key}}</option>
          </select>
        </div>
      </div>
      <div v-if="dataJSON.makes[index]" class="model-select-container">
        <span>Modell</span>
        <div class="model-select">
          <font-awesome-icon class="faChevron" :icon="chevron"></font-awesome-icon>
          <select v-model="dataJSON.models[index]" name="tst2" id="2">
            <option v-for="model in cars[dataJSON.makes[index]]">{{model}}</option>
          </select>
        </div>
      </div>
    </div>
    <button @click="addCar"><font-awesome-icon class="faPlus" :icon="plus"></font-awesome-icon> Weitere Fahrzeuge hinzufügen</button>
  </div>
</template>

<script>
  import {cars} from '../utils/dbMock.js'
  import FontAwesomeIcon from '@fortawesome/vue-fontawesome';
  import {faChevronDown} from "@fortawesome/fontawesome-free-solid"
  import {faPlus} from "@fortawesome/fontawesome-free-solid"


  export default {
    name: 'CarSelect',
    components: {
      FontAwesomeIcon
    },
    data() {
      return {
        cars: cars,
        dataJSON: {
          makes: [''],
          models: ['']
        },
      }
    },
    computed: {
      chevron() {
        return faChevronDown
      },
      plus(){
        return faPlus
      }
    },
    updated: function () {
      this.$emit('change', JSON.parse(JSON.stringify(this.dataJSON)))
    },
    methods: {
      addCar() {
        this.dataJSON.makes.push('');
        this.dataJSON.models.push('');
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  .container {
    width: 100%;
    margin-bottom: 25px;
    .car-select {

      display: flex;
      flex-direction: row;
      justify-content: left;
      margin-bottom: 15px;
      div {
        width: 40%;
        margin-right: 10%;
        div {
          width: 100%;
          height: 30px;
          border-radius: 6px;
          position: relative;
          background: #e6e6eb;
          overflow: hidden;
          .faChevron {
            position: absolute;
            color: #7c7f87;
            height: 60%;
            top: 50%;
            right: 2%;
            transform: translateY(-50%);
            pointer-events: none;
          }
          select {
            width: 100%;
            height: 100%;
            padding-left: 15px;
            -webkit-appearance: none;
            background: transparent;
            border: none;
            &:focus{
              outline: none;
            }
          }
        }
      }
    }
    button {
      background: transparent;
      border: none;
      cursor: pointer;
      &:focus{
        outline: none;
      }
      .faPlus{
        color: #f28022;
      }
    }
  }
</style>
