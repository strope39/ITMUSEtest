<template>
  <div class="search">
    <div class="search__form">
      <div class="search__form-header">Поиск по категориям:</div>
      <form @submit.prevent class="search__form-form">
        <div class="search__form-column">
          
          <label for="region" class="search__form-label">Регион</label>
          <input type="text" class="search__form-area" id="region" placeholder="Выберите регион"
            @click="selectRegionActive(true)"
            @input="findRegion"
            v-bind:value="selectedRegion"
            >
          
          <div class="area__select" v-show="displayRegionList">
            <ul class="area__select-list">
              <li class="area__select-item" v-for="region of selectedRegionList" :key="region" @click="selectedRegionHandler"> {{region}} </li>
            </ul>
          </div>
        </div>
        <div class="search__form-column">
          <label for="city" class="search__form-label">Город</label>
          <input type="text" class="search__form-area" id="city" placeholder="Выберите город"
          @click="selectCityActive(true)"
          @input="findCity"
          v-bind:value="selectedCity">
          <div class="area__select" v-show="displayCityList">
            <ul class="area__select-list">
              <li class="area__select-item" v-for="city of selectedCityList" :key="city" @click="selectedCityHandler"> {{city}} </li>
            </ul>
          </div>
        </div>
        <div class="search__form-column">
          <label for="company" class="search__form-label">Компания</label>
          <input type="text" class="search__form-area" id="company" placeholder="Выберите организацию"
          @click="selectCompanyActive(true)"
          @input="findCompany"
          v-bind:value="selectedCompany"
          >
          <div class="area__select" v-show="displayCompanyList">
            <ul class="area__select-list">
              <li class="area__select-item" v-for="company of selectedCompanyList" :key="company" @click="selectedCompanyHandler"> {{company}} </li>
            </ul>
          </div>
        </div>
      </form>
    </div>
    <Result v-bind:jobs="companyVacancies" v-bind:company="selectedCompany"/>
  </div>
</template>

<script>

import Result from './Result.vue'

export default {
  name: 'TestForm',
  props: {
    vacancies: Array
  },
  components: {
    Result
  },
  data() {
    return {
      regionList: [],
      cityList: [],
      companyList: [],
      selectedRegion: "",
      selectedCity: "",
      selectedCompany: "",
      displayCompanyList: false,
      displayCityList: false,
      displayRegionList: false,
      regionVacancies: [],
      companyVacancies: []

    }
  },
  watch: {
    vacancies: function (vacancies) {
      let regionSet = new Set(vacancies.map((i) =>{
        if (i.regionname !== null) {
          return i.regionname
        }
      }))
      regionSet.delete(undefined)
      console.log (regionSet)  
      this.regionList = Array.from(regionSet).sort((a, b) => a.localeCompare(b));
    },
    selectedRegion: function (){
      this.selectedCity = "";
      if (this.selectedRegion){
      this.regionVacancies = this.vacancies.filter(i => i.regionname == this.selectedRegion )
      let citySet = new Set(this.regionVacancies.map((i) =>{
        if (i.placetitle !== null) {
          return i.placetitle
        }
      }))
      citySet.delete(undefined)
      console.log (citySet)  
      this.cityList = Array.from(citySet).sort((a, b) => a.localeCompare(b))
      }
    },
    selectedCity: function (){
      this.selectedCompany = "";
      if (this.selectedCity){
      this.companyVacancies = this.regionVacancies.filter(i => i.placetitle == this.selectedCity )
      let companySet = new Set(this.companyVacancies.map((i) =>{
        if (i.clientname !== null) {
          return i.clientname
        }
      }))
      companySet.delete(undefined)
      console.log (companySet)  
      this.companyList = Array.from(companySet).sort((a, b) => a.localeCompare(b))
      }
    }

    
  },
  computed: {
    selectedRegionList() {
      return this.regionList.filter(region => {
        return region.toLowerCase().includes(this.selectedRegion.toLowerCase())
      })
    },
    selectedCityList() {
      return this.cityList.filter(city => {
        return city.toLowerCase().includes(this.selectedCity.toLowerCase())
      })
    },
    selectedCompanyList() {
      return this.companyList.filter(company => {
        return company.toLowerCase().includes(this.selectedCompany.toLowerCase())
      })
    },

  },
  methods: {
    selectedRegionHandler: function (event) {
      this.selectedRegion = event.target.outerText
      this.selectRegionActive(false)
      console.log (event.target.outerText)
    },
    selectedCityHandler: function (event) {
      this.selectedCity = event.target.outerText
      this.selectCityActive(false)
      console.log (event.target.outerText)
    },
    selectedCompanyHandler: function (event) {
      this.selectedCompany = event.target.outerText
      this.selectCompanyActive(false)
      console.log (event.target.outerText)
    },
    selectRegionActive: function (cond) {
      this.displayRegionList = cond
    },
    selectCityActive: function (cond) {
      this.displayCityList = cond
    },
    selectCompanyActive: function (cond) {
      this.displayCompanyList = cond
    },
    findRegion: function (event) {
      this.selectedRegion = event.target.value
      console.log (this.selectedRegion)
    },
    findCity: function (event) {
      this.selectedCity = event.target.value
      console.log (this.selectedCity)
    },
    findCompany: function (event) {
      this.selectedCompany = event.target.value
      console.log (this.selectedCompany)
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.search {
  height: 100%;
  margin: 0 auto;
  padding: 50px;
  display: flex;
  
}

.search__form {
  max-width: 350px;
  
}

.search__form-header {
  padding-bottom: 50px;
  font-size: 2.3rem;
  
}

form {
  background-color: white;
  border: 1px white solid;
  border-radius: 5px;
  padding: 1rem 0.5rem;

}

label, input {
  display: block;
  margin-top: 1rem;
}

.search__form-column {
  position: relative;
  width: 100%;
  
}

input {
  z-index: 1;
  width: 100%;
  height: 40px;
  padding: 10px;
  border: 1px #a7a7a7 solid;
  border-radius: 2px;
  font-weight: 600;
}


label {
  position: absolute;
  top: -22px;
  left: 10px;
  z-index: 2;
  font-size: 0.7rem;
  color: #a7a7a7;
  padding: 0 6px;
  background-color: #fff;

}

ul {
  list-style: none;
}
.area__select {
  position: absolute;
  top: 40px;
  z-index: 10;
  background-color: #fff;
  max-height: 300px;
  overflow-x: scroll;

  
}
.area__select-list {
  border: 1px #a7a7a7 solid
}

.area__select-item {
  width: 100%;
  height: 20px;
  cursor: pointer;
}

.area__select-item button {
  border: none;
  cursor: pointer;
}

.selected {
  background-color: aqua;
}

.area__select-item:hover {
  background-color: aqua;
  
}

</style>
