<template>
  <div class="container">
    <div id="jumb" class="row justify-content-center">
      <div class="col-lg-4 col-md-4 col-sm-4">             
        <input type="text" v-model ='boxOne' id ="basic-addon2nd" required=true  class=" form-control rounded-0" placeholder="Crypto QTY" aria-label="Username" aria-describedby="basic-addon1">
      </div><br>
      <div class="col-lg-4 col-md-4 col-sm-4">
        <select class="btn w-100 h-100" @change="getData">
          <option>Select Coin</option>
          <option :key="short.id" v-for="short in shortCode" :value="short" >{{short}}</option>
        </select>
      </div><br>
      <div class="col-lg-4 col-md-4">
        <input type="text" id ="basic-addon2nd" class=" form-control rounded-0"  disabled :placeholder='boxTwo'>
      </div>
      <footer>
        <h4 id='foot'>&copy; {{date.getFullYear()}} iamdyt.</h4>
      </footer>
    </div>
  
</div>
</template>
<script>
  import {coin} from '../assets/Coin.js';
  import axios from 'axios';
export default {
  data(){
    return{
      date: new Date(),
      shortCode:coin,
      boxOne:1,
      boxTwo:'NGN',
      coinPrice:0,
      usdPrice:''
    }
  },

 mounted(){
   this.getUsdNaira();
 },
 watch:{
   boxOne(newValue,oldValue){
     this.boxTwo = `₦${(newValue * parseFloat(this.coinPrice) * this.usdPrice).toFixed(2)}`;
   }
},
  methods:{
    //Function get called on Mounted to get dollar-Naira rate
    getUsdNaira(){
     axios.get(`https://free.currconv.com/api/v7/convert?q=USD_NGN&compact=ultra&apiKey=44d63bd5d10556a1a8e2`) 
      .then(result=>{
        this.usdPrice = result.data.USD_NGN
        
      }).catch(error =>{
          alert("Please Refresh or Check your Internet Connection")
        })
     
    },
  // Function get called onSelecting new option/coin
    getData(event){
      let val = event.target.value.toLowerCase();
      axios.get(`https://api.cryptonator.com/api/ticker/${val}-usd`)
        .then(response=>{
          this.coinPrice = response.data.ticker.price;
          this.boxTwo =`₦${(this.boxOne * parseFloat(this.coinPrice * this.usdPrice).toFixed(2))}`;
        })

        
    }
   
   } 
  
  }
  
</script>

<style scoped>
  #jumb{
    margin-top: 10em;
  }
 #basic-addon2nd{
    padding: 2em;
    
  }
#basic-addon2nd::placeholder{
  color:#143441;
  font-family: 'Titillium Web', sans-serif;
  font-size:1.5em;
}
input{
  color:#143441;
  font-family: 'Titillium Web', sans-serif;
  font-size:1.4em;
}
select{
  border:1px solid #143441;
  color:#0D1F21;
  font-family: 'Titillium Web', sans-serif;
  font-size:1.5em;
}

footer{
  margin-top:15em;
  color:#143441;
  font-family: 'Comfortaa', cursive;
}
</style>
