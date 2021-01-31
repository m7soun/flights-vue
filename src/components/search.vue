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
    <div v-if="data != null">

      <div v-for="item in data" :key="item" class="card">

        <div class="card_heading">

          <h2>Activity</h2>

        </div>

        <div style="margin: auto;
  width: 50%;
  " class="card_thumbnail">
          <h1>{{ item.flight_status }}</h1>

        </div>

        <div class="card_trip">

          <div class="trip_from">

            <h1>{{ item.departure.iata }}</h1>
            <h2>{{ item.departure.airport }}</h2>

          </div>

          <div class="trip_icon">

            <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/553328/From.png"/>

          </div>

          <div class="trip_to">

            <h1>{{ item.arrival.iata }}</h1>
            <h2>{{ item.arrival.airport }}</h2>

          </div>

        </div>

        <div class="card_divider">

          <div class="divider_left divider_hole">

          </div>

          <div class="divider">

          </div>

          <div class="divider_right divider_hole">

          </div>

        </div>

        <div class="card_seating">

          <div class="seating_passenger">

            <h2>Airline</h2>

            <h3>{{ item.airline.name }}</h3>

          </div>

          <div class="seating_seat">

            <h2>Aircraft</h2>
            <h3 v-if="item.aircraft != null" :key="item.aircraft.registration">{{ item.aircraft.registration }}</h3>
            <h3 v-else>not define</h3>

          </div>

        </div>

        <div class="card_details">

          <div class="details_flight">

            <h2>Flight Number</h2>

            <h3>{{ item.flight.number }}</h3>

          </div>

          <div class="details_date">

            <h2>Flight IATA</h2>

            <h3>{{ item.flight.iata }}</h3>

          </div>

          <div class="details_time">

            <h2>Flight ICAO</h2>

            <h3>{{ item.flight.icao }}</h3>

          </div>

        </div>

      </div>

    </div>
  </div>

</template>

<script>
import axios from "axios"

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
        axios.get('http://127.0.0.1:8000/api/v1/flights', {
          params: {
            flight_number: this.flightNumber,
            flight_iata: this.flightIata,
            flight_icao: this.flightIcao
          }
        }).then(response => {
          this.error = null
          this.data = response.data.flights.data
        }).catch(err => {
          err
          this.data = null;
          this.error = 'Something went wrong'
        });
      }

    }
  }
}
</script>

<style>
@import '../assets/styles/search.css';
</style>