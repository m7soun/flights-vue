<template>
  <div class="flight" id="flightbox">

    <div id="flight-depart">
      <div class="info-box">
        <label for="">Flight Number</label>
        <input type="text" id="dep-from" v-model="flightNumber"/>
      </div>
      <div class="info-box">
        <label for="">Flight IATA</label>
        <input type="text" id="dep-from" v-model="flightIata"/>
      </div>
      <div class="info-box">
        <label for="">Flight ICAO</label>
        <input type="text" id="dep-from" v-model="flightIcao"/>
      </div>
    </div>
    <div id="flight-search">
      <div class="info-box">
        <input v-on:click="fetch()" type="submit" id="search-flight" value="SEARCH FLIGHTS"/>
      </div>
    </div>
  </div>

</template>

<script>
import axios from "axios"
import { bus } from '../main'

export default {
  name: "home",
  data: () => ({
    flightNumber: null,
    flightIata: null,
    flightIcao: null,
    error: null,
    data: null,
  }),
  methods: {
    fetch() {
      if (this.flightNumber == null && this.flightIata == null && this.flightIcao == null) {
        this.$alert("One of the fields must be filled", 'Oops!', 'error');
      } else {
        this.loading = true
        axios.get('http://127.0.0.1:8000/api/v1/flights', {
          params: {
            flight_number: this.flightNumber,
            flight_iata: this.flightIata,
            flight_icao: this.flightIcao
          }
        }).then(response => {
          this.error = null
          this.data = response.data
          bus.$emit('data',this.data)

        }).catch(err => {
          err
          this.data = null;
          this.$alert("Something went wrong", 'Oops!', 'error');
        });
      }

    }
  }
}
</script>

<style>
@import '../assets/styles/search.css';
</style>