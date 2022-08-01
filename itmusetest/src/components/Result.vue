<template>
  <div class="result">
    <div class="result__header">Найдено: {{jobsList.length}} вакансии</div>
    <div class="result__body">
    <div class="result__items">
     <div class="result__items-item" v-for="item in jobsList" :key="item.id">
      <div class="item__city">{{item.placetitle}}</div>
      <div class="item__name">{{item.proftitle}}</div>
      <hr>
      <div class="item__salary">{{item.salary_volume_ex}}</div>
      <div class="item__direction">{{item.directiontitle}}</div>
      <div class="item__company">{{item.clientname}}</div>
      <button class="btn__details">Подробнее</button>
      <button @click="showModal" class="btn__respond">Откликнуться</button>
      </div>
    </div>
    </div>
  <Modal v-if="modalShow" @closeModal="closeModal"/>
  </div>
  
</template>

<script>

import Modal from './Modal.vue'

export default {
  name: 'ResultItems',
  components: {
    Modal
  },
  props: {
    jobs: Array,
    company: String
  },
  data() {
    return {
      jobsList: [],
      modalShow: false

    }
  },
  watch: {
    company: function () {
      this.jobsList = this.jobs.filter( i => i.clientname == this.company)
      console.log (this.jobsList)
    },
  },
  methods: {
    showModal() {
      this.modalShow = true
    },
    closeModal() {
      this.modalShow = false
    },
  },
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>

.result {
  padding: 30px;
}

.result__header {
  font-size: 2rem;
  margin: 5px;

}
.result__items {
  display: flex;
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
}
.result__items-item {
  margin: 15px 10px;
  padding: 15px;
  min-width: 300px;
  height: 350px;
  background-color: #fff;
  border: 1px white solid;
  border-radius: 3px;
  
}

.item__city {
  font-size: 0.8rem;
  color: #a7a7a7;
  padding-bottom: 10px;
}
.item__name {
  font-size: 1.5rem;
  padding-top: 10px;
  padding-bottom: 20px;

}

.item__salary {
  padding-top: 20px;
  padding-bottom: 10px;
  font-weight: 600;

}
.item__direction {
  padding: 10px 0;
  font-weight: 600;

}
.item__company {
  padding: 10px 0;
  font-weight: 600;
}
.btn__details {
  padding: 10px;
  border: 2px #fd7f23 solid;
  border-radius: 3px;
  color: #fd7f23;
  width: 100%;
}

.btn__respond {
  padding: 10px;
  width: 100%;
  border: 2px #fd7f23 solid;
  background-color: #fd7f23;
  color: white;
  border-radius: 3px;
}

button {
  display: block;
  margin: 10px auto;
  cursor: pointer;
  font-weight: 600;
}

</style>  