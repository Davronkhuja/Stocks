<script> 
import axios from 'axios'

export default {
  name: 'Stocks',
  data() {
    return{
      stock: [],
      errors: [],
      selected: ''
    }
  },
  created(){
    axios.get('https://financialmodelingprep.com/api/v3/profile/AAPL,NVDA,TSLA,AMD,INTC,MDB,SPCE,V,DAL,DOCU,OKTA,AMZN,PINS,TRIP,GDDY,DIS,MCD,NOK,UPWK,IBM,FB,ZM,OZON,NFLX,EA,HLT,H,CCL?apikey=6c9be8fcb7df7894ba5ae48be14935fc')
    .then(response => {
      this.stock = response.data
      console.log(response);
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<template>
  <div class="stock">
    <div class="stock-item" v-for="value in stock" :key="value.stock">
      <div class="stock-item_info">
        <div class="stock-item_cover">
          <img :src="value.image" :alt="value.companyName">
        </div>
        <h3 class="stock-item_title">
          {{ value.companyName }}
          <span>{{ value.symbol }}</span>
        </h3>
      </div>
      <span class="stock-item_price">{{ value.price }} $</span>
    </div>
  </div>
  <h3>Get Info</h3>
  <select v-model="selected">
    <option value="" disabled>Select Company</option>
    <option :value="value.description" v-for="value in stock" :key="value.stock">{{ value.companyName }}</option>
  </select>
  <div class="info">
    {{ selected }}
  </div>
</template>

<style scoped>
</style>
