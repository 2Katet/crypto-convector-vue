<template>
  <h1>CRYPTO</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite" :getFromFavs="getFromFavs"/>
  <p v-if="error" className="error">{{ error }}</p>
  <p v-if="result" className="result-text">{{ result }}</p>
  <Favorit :favs="favs" v-if="this.favs.length > 0" :getFromFavs="getFromFavs"/>

  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
  </div>
</template>

<script>

import axios from 'axios';
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Favorit from './components/Favorit.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
  data() {
    return {
      amount: 0,
      cryptoFirst: '',
      cryptoSecond: '',
      error: '',
      result: 0,
      favs:[]
    }
  },
  components: {
    Input, Selector, Favorit
  },
  computed: {
  },
  methods: {
    getFromFavs(index){
      this.cryptoFirst = this.favs[index].from
      this.cryptoSecond = this.favs[index].to
    },
    favourite (){
      if(this.cryptoFirst == '' || this.cryptoSecond == '') return
      this.favs.push({
        from: this.cryptoFirst,
        to: this.cryptoSecond,
      })
    },
    changeAmount(val) {
      this.amount = val
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val
    },
    async convert() {
      // Проверка суммы
      if (this.amount <= 0) {
        this.error = 'Введите число больше за ноль';
        return;
      } else if (this.cryptoFirst == '' || this.cryptoSecond == '') {
        this.error = 'Выберите валюту';
        return;
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = 'Выберите другую валюту';
        return;
      }
      this.error = '';

      await convert.ready();

      // Условия конвертации
      if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH')
        this.result = convert.BTC.ETH(this.amount);
      else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC')
        this.result = convert.ETH.BTC(this.amount);
      else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC')
        this.result = convert.USDT.BTC(this.amount);
      else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT')
        this.result = convert.BTC.USDT(this.amount);
      else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT')
        this.result = convert.ETH.USDT(this.amount);
      else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH')
        this.result = convert.USDT.ETH(this.amount);
    }
  }
}
</script>




<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
}

.error {
  color: rgb(255, 255, 255);
  font-size: 15px;
}

.result-text {
  font-family: 'Nabla', cursive;
  font-size: 2em;
}
</style>
