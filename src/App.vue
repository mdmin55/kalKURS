<script>
import Input from './components/Input.vue'
import Selector from './components/Selector.vue'
import Freecurrencyapi from '@everapi/freecurrencyapi-js';
// import axios  from 'axios';
export default{
  components:{Input, Selector },
  data(){
    return {
      amount: 0,
      kursFirst:'',
      kursSecond:'',
      error: '',
      freecurrencyapi: null,
     result: 0
    }
  },
  created() {
    this.freecurrencyapi = new Freecurrencyapi('fca_live_5pLEvj32EGudQx3HCxiYfIpN2mZnsOTN0OWMsg5i');
    this.fetchExchangeRate();
  },
  methods:{
  changeAmount(val){
    this.amount= val
  },
  setKursFirst(val){
    this.kursFirst =val
  },
  setKursSecond(val){
    this.kursSecond =val
  },
  fetchExchangeRate() {

    if (this.kursFirst === 'RUB' && this.kursSecond === 'USD') {
    this.freecurrencyapi.latest({
      base_currency: 'RUB',
      currencies: 'USD'
    }).then(response => {
      this.result = response.data.USD * this.amount;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });} 
    else if(this.kursFirst === 'RUB' && this.kursSecond === 'EUR'){
    this.freecurrencyapi.latest({
      base_currency: 'RUB',
      currencies: 'EUR'
    }).then(response => {
      this.result = response.data.EUR * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });}  
    else if(this.kursFirst === 'RUB' && this.kursSecond === 'KRW'){
    this.freecurrencyapi.latest({
      base_currency: 'RUB',
      currencies: 'KRW'
    }).then(response => {
      this.result = response.data.KRW * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });}

    else if(this.kursFirst === 'USD' && this.kursSecond === 'KRW'){
    this.freecurrencyapi.latest({
      base_currency: 'USD',
      currencies: 'KRW'
    }).then(response => {
      this.result = response.data.KRW * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });} 
    else if(this.kursFirst === 'USD' && this.kursSecond === 'RUB'){
    this.freecurrencyapi.latest({
      base_currency: 'USD',
      currencies: 'RUB'
    }).then(response => {
      this.result = response.data.RUB * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });}
    else if(this.kursFirst === 'USD' && this.kursSecond === 'EUR'){
    this.freecurrencyapi.latest({
      base_currency: 'USD',
      currencies: 'EUR'
    }).then(response => {
      this.result = response.data.EUR * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });} 
    
    else if(this.kursFirst === 'EUR' && this.kursSecond === 'USD'){
    this.freecurrencyapi.latest({
      base_currency: 'EUR',
      currencies: 'USD'
    }).then(response => {
      this.result = response.data.USD * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });}
    else if(this.kursFirst === 'EUR' && this.kursSecond === 'KRW'){
    this.freecurrencyapi.latest({
      base_currency: 'EUR',
      currencies: 'KRW'
    }).then(response => {
      this.result = response.data.KRW * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });} 
    else if(this.kursFirst === 'EUR' && this.kursSecond === 'RUB'){
    this.freecurrencyapi.latest({
      base_currency: 'EUR',
      currencies: 'RUB'
    }).then(response => {
      this.result = response.data.RUB * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });}


    else if(this.kursFirst === 'KRW' && this.kursSecond === 'EUR'){
    this.freecurrencyapi.latest({
      base_currency: 'KRW',
      currencies: 'EUR'
    }).then(response => {
      this.result = response.data.EUR * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });}
    else if(this.kursFirst === 'KRW' && this.kursSecond === 'USD'){
    this.freecurrencyapi.latest({
      base_currency: 'KRW',
      currencies: 'USD'
    }).then(response => {
      this.result = response.data.USD * this.amount ;
    }).catch(error => {
      this.error = 'Error fetching exchange rate: ' + error;
    });} 
    else if(this.kursFirst === 'KRW' && this.kursSecond=== 'RUB'){
    this.freecurrencyapi.latest({
      base_currency: 'KRW',
      currencies: 'RUB'
    }).then(response => {
      this.result = response.data.RUB * this.amount ;
    }).catch(error => {cd
      this.error = 'Error fetching exchange rate: ' + error;
    });}
  else {
    this.error = ' $ Выберите из столбика с лева волюту, которую нужно перевести, а с права, ту в которую нужно $';
  }
     
    },
  convert(){
    this.fetchExchangeRate();

if(this.amount <= 0){
  this.error='Напишите число > 0';
  return;
}else if(this.kursFirst === this.kursSecond){
  this.error='Выберите разные волюта';
  return;
} else if(this.kursFirst === ''){
  this.error='Выберите КАКУЮ волюту нужно расчитать';
  return;
}else if(this.kursSecond === ''){
  this.error='Выберите в какую волюту нужно расчитать';
  return;
}
 this.error = '';
}
}
}
</script>

<template>
  <h1>kalKURS</h1> 
  <Input :changeAmount="changeAmount" :convert="convert" :fetchExchangeRate="fetchExchangeRate"/>
  <p v-if="error !=''" >{{ error }}</p>
  <p v-if="result !=0 " >{{ result  }}</p>
  <div class="blocs">
    <Selector :setKurs="setKursFirst" />
    <Selector :setKurs="setKursSecond"/>
  </div>

</template>

<style scoped>
.blocs{
  display: flex;
  justify-content: space-around;
  margin: 0 auto;
  width: 700px;
}
p{
  font-size: 20px;

}
</style>
