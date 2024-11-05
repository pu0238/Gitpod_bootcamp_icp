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
  <main class="container mx-auto">
  <table class="w-full">
    <thead class="text-lime-500 border-solid border-b-2 border-lime-500">
      <tr>
        <th scope="col">Waluta</th>
        <th scope="col">Kod</th>
        <th scope="col">Cena</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="kurs in kursy" class="border-solid border-b-[1px] border-lime-500">
        <th scope="row" class="p-2">{{kurs.currency}}</th>
        <td class="p-2">{{kurs.code}}</td>
        <td class="p-2">{{kurs.mid}}</td>
      </tr>
    </tbody>  
  </table>

  </main>
</template>
