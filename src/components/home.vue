<template>
  <div>
    <div>
      <div style="margin: 5px" v-if="data != null">
        <table border="1px">
          <tr>
            <th>flight date</th>
            <th>flight status</th>
            <th>departure</th>
            <th>arrival</th>
            <th>airline</th>
            <th>aircraft</th>
          </tr>
          <tr v-for="item in data" :key="item">

            <td :key="item.flight_date">{{ item.flight_date }}</td>
            <td :key="item.flight_status">{{ item.flight_status }}</td>
            <td :key="item.departure">{{ item.departure.airport }}</td>
            <td :key="item.arrival.airport">{{ item.arrival.airport }}</td>
            <td :key="item.airline.name">{{ item.airline.name }}</td>
            <td v-if="item.aircraft != null" :key="item.aircraft.registration">{{ item.aircraft.registration }}</td>
            <td v-else>not define</td>
          </tr>
        </table>
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
        this.$alert("One of the fields must be filled",'Oops!','error');

        // this.error = 'One of the filed is required'
      } else {
        axios.get('http://127.0.0.1:8000/api/v1/flights', {
          params: {
            flight_number: this.flightNumber,
            flight_iata: this.flightIata,
            flight_icao: this.flightIcao
          }
        }).then(response => {
          this.error = null
          this.data = response.data.data
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

<style scoped>

</style>