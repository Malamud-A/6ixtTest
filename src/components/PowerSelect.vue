<template>
  <div class="leistung-container">
    <div class="from-select">
      <font-awesome-icon class="faChevron" :icon="chevron"></font-awesome-icon>
      <select v-model="dataJSON.from" name="leistug-from" id="leistung-from">
        <option disabled>von</option>
        <option v-for="n in leistung[units]">{{n + ' ' + units}}</option>
      </select>
    </div>
    <div class="to-select">
      <font-awesome-icon class="faChevron" :icon="chevron"></font-awesome-icon>
      <select v-model="dataJSON.to" name="leistug-to" id="leistung-to">
        <option disabled>bis</option>
        <option v-for="n in leistung[units]" :disabled="n < dataJSON.from.split(' ')[0]">{{n + ' ' + units}}</option>
      </select>
    </div>
    <RadioButton className="units-radio" initial="PS" :values="['PS', 'kW']" model="units" @change="updateUnits"></RadioButton>
  </div>
</template>

<script>
  import {leistung} from "../utils/dbMock.js";
  import FontAwesomeIcon from '@fortawesome/vue-fontawesome';
  import {faChevronDown} from "@fortawesome/fontawesome-free-solid"
  import RadioButton from './RadioButton'

  export default {
    name: "PowerSelect",
    components: {
      FontAwesomeIcon,
      RadioButton
    },
    data() {
      return {
        leistung: leistung,
        units: 'PS',
        dataJSON: {
          from: 'von',
          to: 'bis',
        },

      }
    },
    computed: {
      chevron() {
        return faChevronDown
      }
    },
    // beforeMount: function () {
    //   this.dataJSON.from = `${this.leistung[this.units][0]} ${this.units}`;
    //   this.dataJSON.to = `${this.leistung[this.units][1]} ${this.units}`;
    // },
    updated: function () {
      this.$emit('change', JSON.parse(JSON.stringify(this.dataJSON)));
    },
    methods: {
      updateUnits(value) {
        this.units = value.checked;
        this.dataJSON.from = `von`;
        this.dataJSON.to = `bis`;
      }
    }
  }
</script>

<style lang="scss" scoped>
  .leistung-container{
    width: 90%;
    display: flex;
    flex-flow: row;
    justify-content: space-between;
    margin-bottom: 15px;
    .from-select, .to-select {
      width: 30%;
      height: 25px;
      border-radius: 3px;
      position: relative;
      background: #e6e6eb;
      overflow: hidden;
      select{
        position: relative;
        width: 100%;
        height: 100%;
        -webkit-appearance: none;
        padding-left: 10px;
        background: transparent;
        border: none;
        &:focus{
          outline: none;
        }
      }
      .faChevron{
        position: absolute;
        color: #7c7f87;
        height: 60%;
        top: 50%;
        right: 3%;
        transform: translateY(-50%);
        pointer-events: none;
      }
    }
    .units-radio{
      width: 20%;
      display: flex;
      flex-flow: row;
      justify-content: space-between;
    }
  }
</style>
