<template>
  <div id="app">
    <div class="form-container">
      <h3>Marke, Modell</h3>
      <div class="separator"></div>
      <CarSelect @change="onCarSelectChange"/>
      <h3>Motor</h3>
      <div class="separator"></div>
      <span class="section-caption">Kraftstoffart</span>
      <div class="checkbox-section">
        <CheckBox model="Motor" value="Benzin" @change="checkboxChange"></CheckBox>
        <CheckBox model="Motor" value="Diesel" @change="checkboxChange"></CheckBox>
        <CheckBox model="Motor" value="Elektro" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Motor" value="Hybrid" @change="checkboxChange"></CheckBox>
        <CheckBox model="Motor" value="Gas LPM/CNG" @change="checkboxChange"></CheckBox>
        <CheckBox model="Motor" value="Andere" @change="checkboxChange"></CheckBox>
      </div>
      <span class="section-caption">Getriebe</span>
      <div class="checkbox-section">
        <CheckBox model="Getriebe" value="Shcaltgetriebe" @change="checkboxChange"></CheckBox>
        <CheckBox model="Getriebe" value="Halbautomatik" @change="checkboxChange"></CheckBox>
        <CheckBox model="Getriebe" value="Automatik" @change="checkboxChange"></CheckBox>
      </div>
      <span class="section-caption">Liestung</span>
      <PowerSelect @change="leistungChange"></PowerSelect>
      <h3>Standort</h3>
      <div class="separator"></div>
      <span class="section-caption">Location in Germany</span>
      <div class="checkbox-section">
        <CheckBox model="Standort" value="Garching bei München" @change="checkboxChange"></CheckBox>
        <CheckBox model="Standort" value="Nürnberg" @change="checkboxChange"></CheckBox>
        <CheckBox model="Standort" value="Frankfurt am Main" @change="checkboxChange"></CheckBox>
        <CheckBox model="Standort" value="Berlin" @change="checkboxChange"></CheckBox>
        <CheckBox model="Standort" value="Eching bei München" @change="checkboxChange"></CheckBox>
      </div>
      <h3>Fahrzeugtyp</h3>
      <div class="separator"></div>
      <span class="section-caption">Available vehicle types</span>
      <div class="fahrzeugtyp-filter">
        <CheckboxWithImage icon="cabrio" value="Cabrio" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="suv" value="Geländewagen" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="kleinwagen" value="Kleinwagen" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="kombi" value="Kombi" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="limousine" value="Limousine" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="coupe" value="Coupe" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="van" value="Van/Minibus" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage icon="pickup" value="Pickup" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
        <CheckboxWithImage value="Andere" model="Fahrzeugtyp"
                           @change="checkboxChange"></CheckboxWithImage>
      </div>
      <div class="seats-doors-container">
        <div class="seats-from-select">
          <span>Anzahl Sitzplatze</span>
          <font-awesome-icon class="faChevron" :icon="faChevronDown"></font-awesome-icon>
          <select v-model="formData.AnzahlSitzplatze.von">
            <option disabled>von</option>
            <option value="2">2</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8</option>
          </select>
        </div>
        <div class="seats-to-select">
          <font-awesome-icon class="faChevron" :icon="faChevronDown"></font-awesome-icon>
          <select v-model="formData.AnzahlSitzplatze.bis">
            <option disabled>bis</option>
            <option value="2">2</option>
            <option value="4">4</option>
            <option value="5">5</option>
            <option value="6">6</option>
            <option value="7">7</option>
            <option value="8">8</option>
          </select>
        </div>
        <div class="doors-select">
          <span>Anzahl Turen</span>
          <font-awesome-icon class="faChevron" :icon="faChevronDown"></font-awesome-icon>
          <select v-model="formData.AnzahlTuren">
            <option value="Beliebig">Beliebig</option>
            <option value="2/3">2/3</option>
            <option value="4/5">4/5</option>
            <option value="6/7">6/7</option>
          </select>
        </div>
      </div>
      <h3>Außenfarbe</h3>
      <div class="separator"></div>
      <span class="section-caption">Available colours</span>
      <div class="color-filter">
        <CheckBox backgroundColor="black" model="Außenfarbe" value="Schwarz" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#999999" model="Außenfarbe" value="Grau" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#3a79c2" model="Außenfarbe" value="Blau" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#1ba652" model="Außenfarbe" value="Grun" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#664b18" model="Außenfarbe" value="Braun" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#d9c5a5" model="Außenfarbe" value="Beige" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#e6d520" model="Außenfarbe" value="Gelb" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox backgroundColor="linear-gradient(to bottom, #f2dd3f, #d9ab23)" model="Außenfarbe" value="Gold"
                  @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#f28022" model="Außenfarbe" value="Orange" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#cf021a" model="Außenfarbe" value="Rot" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="#813cbd" model="Außenfarbe" value="Violet" @change="checkboxChange"></CheckBox>
        <CheckBox backgroundColor="linear-gradient(to bottom, #e3e1e1, #c2c0c0)" model="Außenfarbe" value="Silver"
                  @change="checkboxChange"></CheckBox>
        <CheckBox model="Außenfarbe" value="Weiß" @change="checkboxChange"></CheckBox>
        <CheckBox model="Außenfarbe" value="Metallic" @change="checkboxChange"></CheckBox>
      </div>
      <h3>Ausstattung</h3>
      <div class="separator"></div>
      <span class="section-caption">Klimatisierung</span>
      <RadioButton class-name="radiobutton-pair" :values="['Klimaanlange', 'Klimaautomatik']"
                   model="Klimatisierung" @change="radioButtonChange"></RadioButton>
      <span class="section-caption">Innenausstattung</span>
      <div class="checkbox-section">
        <CheckBox model="Innenausstattung" value="Bluetooth" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="BordComputer" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Head-up Display" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Innenausstattung" value="Isofix (Kindersitzbefestigung)" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Multifunktionslenkrad" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Navigationssystem" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Innenausstattung" value="Regensensor" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Schiebedach" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Skisack" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Innenausstattung" value="Standheizung" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Start/Stopp-Automatik" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung" value="Tempomat" @change="checkboxChange"></CheckBox>
      </div>
      <span class="section-caption">Elektr.Verstellb.Sitze</span>
      <RadioButton className="radiobutton-pair" :values="['vorne', 'hinte']" model="ElektrVerstellbSitze"
                   @change="radioButtonChange"></RadioButton>
      <span class="section-caption">Sitzheizung</span>
      <RadioButton className="radiobutton-pair" :values="['vorne', 'hinte']" model="Sitzheizung"
                   @change="radioButtonChange"></RadioButton>
      <span class="section-caption">Sicherhelt</span>
      <div class="checkbox-section">
        <CheckBox model="Sicherheit" value="Allrandtrieb" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sicherheit" value="ESP" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sicherheit" value="Kurvenlicht" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Sicherheit" value="Lichtsensor" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sicherheit" value="Nebelscheinwerfer" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sicherheit" value="Tagfahrlicht" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Sicherheit" value="Traktionskontrolle" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sicherheit" value="Xenonscheinwerfer" @change="checkboxChange"></CheckBox>
      </div>
      <span class="section-caption">Sport</span>
      <div class="checkbox-section">
        <CheckBox model="Sport" value="Sportfahrwerk" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sport" value="Sportpaket" @change="checkboxChange"></CheckBox>
        <CheckBox model="Sport" value="Sportsitze" @change="checkboxChange"></CheckBox>
      </div>
      <span class="section-caption">Extras</span>
      <div class="checkbox-section">
        <CheckBox model="Extras" value="Anhangerkupplung" @change="checkboxChange"></CheckBox>
        <CheckBox model="Extras" value="Leichmetallfelgen" @change="checkboxChange"></CheckBox>
        <CheckBox model="Extras" value="Ponorama-Dach" @change="checkboxChange"></CheckBox>
      </div>
      <span class="section-caption">Innenausstattung</span>
      <div class="checkbox-section">
        <CheckBox model="Innenausstattung2" value="Vollleder" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung2" value="Teilleder" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung2" value="Stoff" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Innenausstattung2" value="Aicantara" @change="checkboxChange"></CheckBox>
        <CheckBox model="Innenausstattung2" value="Andere" @change="checkboxChange"></CheckBox>
      </div>
      <h3>Umwelt</h3>
      <div class="separator"></div>
      <div class="environment-filter">
        <div class="pollution-select">
          <span>Shadstoffklasse ab</span>
          <font-awesome-icon class="faChevron" :icon="faChevronDown"></font-awesome-icon>
          <select v-model="formData.Schadstoffklasse">
            <option value="Beliebe">Beliebe</option>
            <option value="Euro1">Euro1</option>
            <option value="Euro2">Euro2</option>
            <option value="Euro3">Euro3</option>
            <option value="Euro4">Euro4</option>
            <option value="Euro5">Euro5</option>
            <option value="Euro6">Euro6</option>
          </select>
        </div>
        <div class="env-badge-select">
          <span>Umweltplakette ab</span>
          <font-awesome-icon class="faChevron" :icon="faChevronDown"></font-awesome-icon>
          <select v-model="formData.Umweltplaketter">
            <option value="Beliebe">Beliebe</option>
            <option value="4">4 (Grun)</option>
            <option value="3">3 (Gelb)</option>
            <option value="2">2 (Rot)</option>
            <option value="1">1 (Keiner)</option>
          </select>
        </div>
        <CheckBox className="Partikelfilter" model="Partikelfilter" value="Partikelfilter"
                  @change="checkboxChange"></CheckBox>
      </div>
      <h3>Fahrzeughistorie</h3>
      <div class="separator"></div>
      <div class="checkbox-section">
        <CheckBox model="Fahrzeughistorie" value="Nichtraucher-Fahrzeug" @change="checkboxChange"></CheckBox>
        <CheckBox model="Fahrzeughistorie" value="Scheckheftgepflegt" @change="checkboxChange"></CheckBox>
        <CheckBox model="Fahrzeughistorie" value="Jahreswagen" @change="checkboxChange"></CheckBox>
        <br>
        <CheckBox model="Fahrzeughistorie" value="Tageszulassung" @change="checkboxChange"></CheckBox>
        <CheckBox model="Fahrzeughistorie" value="Gebrauchtwagen" @change="checkboxChange"></CheckBox>

      </div>
      <Modal v-if="isModalOpen" @close="openModal" :content="this.$data"></Modal>
    </div>
    <div class="buttons-container">
      <button class="modalButton-top" @click="modalHandler">Show Data</button>
      <button class="modalButton-bot" @click="modalHandler">Show Data</button>
    </div>
    <div v-if="scrolled > 100" @click="scrollToTop" class="toTopButton">
      <font-awesome-icon :icon="faChevronUp"></font-awesome-icon>
    </div>
  </div>
</template>

<script>
  import CarSelect from './components/CarSelect';
  import CheckBox from './components/Checkbox';
  import PowerSelect from './components/PowerSelect';
  import RadioButton from './components/RadioButton';
  import FontAwesomeIcon from '@fortawesome/vue-fontawesome';
  import {faChevronDown} from "@fortawesome/fontawesome-free-solid";
  import {faChevronUp} from "@fortawesome/fontawesome-free-solid";
  import CheckboxWithImage from './components/CheckboxWithImage';
  import Modal from "./components/Modal"

  export default {
    name: 'App',
    components: {
      CarSelect,
      CheckBox,
      PowerSelect,
      RadioButton,
      FontAwesomeIcon,
      CheckboxWithImage,
      Modal
    },
    data() {
      return {
        formData: {
          Brands: [],
          Models: [],
          Motor: [],
          Getriebe: [],
          Leistung: {
            bis: '',
            von: ''
          },
          Standort: [],
          Fahrzeugtyp: [],
          AnzahlSitzplatze: {
            von: 'von',
            bis: 'bis'
          },
          AnzahlTuren: 'Beliebig',
          Außenfarbe: [],
          Klimatisierung: '',
          Innenausstattung: [],
          ElektrVerstellbSitze: '',
          Sitzheizung: '',
          Sicherheit: [],
          Sport: [],
          Extras: [],
          Innenausstattung2: [],
          Schadstoffklasse: 'Beliebe',
          Umweltplaketter: 'Beliebe',
          Partikelfilter: [],
          Fahrzeughistorie: [],
        },
        isModalOpen: false,
        scrolled: 0,
      }
    },
    computed: {
      faChevronDown() {
        return faChevronDown;
      },
      faChevronUp() {
        return faChevronUp;
      },
      modalHandler(){
        return this.openModal.bind(this)
      }
    },
    mounted () {
      document.addEventListener('scroll', this.scrollListener);
    },
    methods: {
      onCarSelectChange(value) {
        this.formData.Brands = value.makes.filter((el, index) => {
          if (value.makes.indexOf(el) !== index) {
            return
          }
          return el;
        });
        this.formData.Models = value.models.filter((el, index) => {
          if (value.models.indexOf(el) !== index) {
            return
          }
          return el;
        });
      },
      checkboxChange(value) {
        let model = this.$data.formData[value.model];
        value.checked ? model.push(value.value) :
          model.splice(model.indexOf(value.value), 1);
      },
      radioButtonChange(value) {
        this.$data.formData[value.model] = value.checked;
        console.log(value);
      },
      leistungChange(value) {
        this.formData.Leistung.bis = value.from;
        this.formData.Leistung.von = value.to;
      },
      scrollToTop() {
        window.scroll({
          top: 0,
          left: 0,
          behavior: "smooth"
        });
      },
      openModal() {
        this.isModalOpen ? this.isModalOpen = false : this.isModalOpen = true;
        console.log(this.$data)
      },
      scrollListener() {
        this.scrolled = window.scrollY;
      }
    }
  }
</script>

<style lang="scss">
  $text-color: #3f3d4f;
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    padding-left: 20%;
    color: $text-color;
    display: flex;
    flex-direction: row;
    .form-container {
      width: 65%;
      display: flex;
      flex-direction: column;
      .separator {
        width: 100%;
        height: 1px;
        background: #d9d9de;
        margin-bottom: 25px;
      }
      .section-caption {
        font-weight: 700;
        margin: 10px 0;
      }
      .checkbox-section {
        display: flex;
        flex-flow: row wrap;
        font-size: 14px;
        & > * {
          width: 30%;
          margin-bottom: 10px;

        }
        @media screen and (max-width: 960px) {
          font-size: 10px;
        }
      }
      .fahrzeugtyp-filter{
        display: flex;
        flex-flow: row wrap;
        & > * {
          margin: 0 0 10px 15px;
        }
      }
      .color-filter {
        display: flex;
        flex-flow: row wrap;
        @media screen and (max-width: 960px) {
          font-size: 10px;
        }
        & > * {
          width: 9%;
          margin-bottom: 10px;
          margin-right: 11px;

        }
      }
      .seats-doors-container, .environment-filter {
        margin-top: 40px;
        div {
          width: 25%;
          height: 25px;
          border-radius: 3px;
          position: relative;
          background: #e6e6eb;
          display: inline-block;
          margin-right: 6%;
          span {
            position: absolute;
            top: -22px;
            font-weight: 700;
            @media screen and (max-width: 960px) {
              font-size: 12px;
              top: -30px;
            }
          }
          select {
            position: relative;
            width: 100%;
            height: 100%;
            -webkit-appearance: none;
            padding-left: 10px;
            background: transparent;
            border: none;
            &:focus {
              outline: none;
            }
          }
          .faChevron {
            position: absolute;
            color: #7c7f87;
            height: 60%;
            top: 50%;
            right: 3%;
            transform: translateY(-50%);
            pointer-events: none;
          }
        }
        .Partikelfilter {
          display: inline;
          margin-bottom: 15px;
        }
      }
      .environment-filter {
        margin-bottom: 25px;
      }
      .radiobutton-pair {
        display: flex;
        flex-flow: row;
        justify-content: space-between;
        width: 50%;
        margin-bottom: 25px;
      }

    }
    .buttons-container{
      width: 30%;
      position: relative;
      button{
        position: absolute;
        width: 75%;
        left: 50%;
        height: 35px;
        border-radius: 30px;
        transform: translateX(-50%);
        border: none;
        text-transform: uppercase;
        color: #fff;
        font-weight: bold;
        background-color: #f28022;
        &.modalButton-bot{
          bottom: 0;
        }
        &.modalButton-top{
          top: 40px;
        }
      }
    }
    .toTopButton{
      position: fixed;
      left: 2%;
      height: 40px;
      width: 40px;
      border-radius: 7px;
      background-color: rgba(0,0,0,0.4);
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      &:hover{
        background-color: rgba(0,0,0,0.6);
      }
    }
  }
</style>
