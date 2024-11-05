<script lang="ts">
import { ref } from 'vue';

export default {
  data() {
    return {
      kursy: []
    }
  },
  methods: {
    async getExchangeRates() {
      const url = `${window.location.origin}/api/exchangerates/tables/a/?format=json`
      const response = await fetch(url);

      const responseJson = await response.json()
      this.kursy = responseJson[0].rates
    }
  },
  async mounted(){
    await this.getExchangeRates();
  }
}
/*
const url = "https://api.nbp.pl/api/exchangerates/tables/a/?format=json"
const response = fetch(url);
*/
</script>

<template>
  <main>
  <table>
    <thead>
      <tr>
        <th scope="col">Waluta</th>
        <th scope="col">Kod</th>
        <th scope="col">Cena</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="kurs in kursy">
        <th scope="row">{{kurs.currency}}</th>
        <td>{{kurs.code}}</td>
        <td>{{kurs.mid}}</td>
      </tr>
    </tbody>  
  </table>

  </main>
</template>
