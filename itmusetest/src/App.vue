<template>
  <div id="app">
    <Test v-bind:vacancies="vacancies"/>
  </div>
</template>

<script>
import Test from './components/Test.vue'


export default {
  name: 'App',
  components: {
    Test
  },
  data () {
    return {
      vacancies: []
    }
  },
  mounted() {
    fetch('https://gsr-rabota.ru/api/v2/GetAllVacancies')
      .then(response => response.json())
      .then(json => this.vacancies = json)
  },
  

}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #f1f2f4;
}

#app {
  width: 100vw;
  height: 100vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  margin: 50px 0;
  
  
  
}
</style>
