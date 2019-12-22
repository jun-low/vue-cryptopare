<template>
  <div class="row">
    <div class="col-md-8">
      <table class="table is-bordered is-striped is-hoverable is-fullwidth">
        <thead>
          <tr class="is-selected">
            <th>#</th>
            <th>Coin</th>
            <th>Name</th>
            <th>Market Cap</th>
            <th>Price</th>
            <th>Volume (24h)</th>
            <th>Circulating Supply</th>
            <th>Open (24h)</th>
            <th>Change PCT (24h)</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(value, key, index) in coins" :key="index">
            <th>{{index+1}}</th>
            <td><img :src="'https://www.cryptocompare.com' + value.USD.IMAGEURL" width="50" height="25"/></td>
            <td>{{key}}</td>
            <td>{{value.USD.MKTCAP}}</td>
            <td>{{value.USD.PRICE}}</td>
            <td>{{value.USD.VOLUME24HOUR}}</td>
            <td>{{value.USD.SUPPLY}}</td>
            <td>{{value.USD.OPEN24HOUR}}</td>
            <td :style="getColor(value.USD.CHANGEPCT24HOUR)">{{value.USD.CHANGEPCT24HOUR}}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

const CRYPTOCOMPARE_API_URI = "https://min-api.cryptocompare.com";
// const COINMARKETCAP_API_URI = "https://api.coinmarketcap.com";
// const BASE_IMAGE_URL = "https://www.cryptocompare.com"

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
    // getCoinData() {
    //   axios.get(COINMARKETCAP_API_URI + "/v1/ticker/?limit=10")
    //   .then((response) => {
    //     console.log('got coinmarket Data')
    //     this.coins = response.data;
    //     console.log(response.data); //
    //   })
    //   .catch((err) => {
    //     console.error(err);
    //   });
    // },
    getCoins() {
      axios.get(CRYPTOCOMPARE_API_URI + '/data/pricemultifull?fsyms=BTC,XRP,ETH,EOS,BCH,LTC,BNB,USDT,DASH,DOGE&tsyms=USD,EUR')
      .then(response => {
        this.coins = response.data.DISPLAY
        // console.log(response)
      })
      .catch(error => {
        console.log(error);
      })
    },
    // getCoinImage: function(symbol) {
    //   try {
    //     return BASE_IMAGE_URL + this.coinData[symbol].USD.IMAGEURL;
    //   } catch (err) {
    //     return "https://upload.wikimedia.org/wikipedia/commons/a/ac/No_image_available.svg"
    //   }
    // },
    getColor: (num) => {
      return num >= 0 ? "color:green;" : "color:red;";
    },
  }
}
</script>

<style></style>