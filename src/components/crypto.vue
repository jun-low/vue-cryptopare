<template>
  <div class="w-full mx-auto p-4">
    <div class="container">
      <table class="table-fixed border-2 border-gray-500 text-left">
        <thead class="border-b border-gray-400 text-gray-800">
          <tr class="font-bold text-sm">
            <th class="bg-gray-400 px-4 py-2 text-gray-800">#</th>
            <th class="bg-gray-400 px-4 py-2 text-gray-800">Coin</th>
            <th class="bg-gray-400 px-4 py-2 text-gray-800">Name</th>
            <th class="w-1/5 bg-gray-400 px-4 py-2 text-gray-800">Market Cap</th>
            <th class="w-1/5 bg-gray-400 px-4 py-2 text-gray-800">Price</th>
            <th class="w-1/5 bg-gray-400 px-4 py-2 text-gray-800">Volume (24h)</th>
            <th class="w-1/4 bg-gray-400 px-4 py-2 text-gray-800">Circulating Supply</th>
            <th class="w-1/5 bg-gray-400 px-4 py-2 text-gray-800">Open (24h)</th>
            <th class="bg-gray-400 px-4 py-2 text-gray-800">Change PCT (24h)</th>
          </tr>
        </thead>
        <tbody class="text-sm py-2">
          <tr class="hover:bg-gray-200" v-for="(value, key, index) in coins" :key="index">
            <th class="px-4">{{index+1}}</th>
            <td class="px-4"><img :src="'https://www.cryptocompare.com' + value.USD.IMAGEURL" width="50" height="25"/></td>
            <td class="px-4">{{key}}</td>
            <td class="px-4">{{value.USD.MKTCAP}}</td>
            <td class="px-4">{{value.USD.PRICE}}</td>
            <td class="px-4">{{value.USD.VOLUME24HOUR}}</td>
            <td class="px-4">{{value.USD.SUPPLY}}</td>
            <td class="px-4">{{value.USD.OPEN24HOUR}}</td>
            <td class="px-4" :style="getColor(value.USD.CHANGEPCT24HOUR)">{{value.USD.CHANGEPCT24HOUR}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

const CRYPTOCOMPARE_API_URI = "https://min-api.cryptocompare.com";

export default {
  name: 'crypto',
  data() {
    return {
      coins: [],
      coinData: {}
    }
  },
  created() {
    this.getCoins();
    setInterval(() => {
      this.getCoins();
    }, 10000);
  },
  methods: {
    getCoins() {
      axios.get(CRYPTOCOMPARE_API_URI + '/data/pricemultifull?fsyms=BTC,XRP,ETH,EOS,BCH,LTC,BNB,USDT,DASH,DOGE&tsyms=USD,EUR')
      .then(response => {
        this.coins = response.data.DISPLAY
      })
      .catch(error => {
        console.log(error);
      })
    },
    getColor: (num) => {
      return num >= 0 ? "color:green;" : "color:red;";
    },
  }
}
</script>

<style></style>
