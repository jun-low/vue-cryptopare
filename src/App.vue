  <template>
  <div id="app" class="container mx-auto p-4 font-mono">
    <h1 class="text-2xl text-gray-800 text-center">Cryptocurrency Compare</h1>
    <div class="container mx-auto">
      <div class="bg-gray-200 m-12 p-12 antialiased text-center font-hairline">
        <p>
          This website indexes the top 10 cryptocurrencies by market cap (how
          much the sum of all coins is collectively worth), and gives you an easy
          way to compare cryptocurrency performance and results every 10 seconds.
        </p>
      </div>
    </div>
    <crypto></crypto>
  </div>
</template>

<script>
import crypto from "./components/crypto";

export default {
  name: 'app',
  components: {
    crypto
  }
}
</script>

<style>
td img {
  width: 25px;
}

.jumbotron p {
  font-size: 1.2em;
}

.jumbotron {
  margin-top: 5em;
  margin-bottom: 5em;
}
</style>
