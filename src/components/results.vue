<template>
    <div v-if="data.flights != null">
        <h1 style="color: black;text-align: center ;">Activities</h1>

        <div v-for="(item,idx) in data.flights" :key="idx" class="card">

            <div class="card_heading">

                <h2>Activity</h2>

            </div>

            <div style="margin: auto;width: 50%;" class="card_thumbnail">
                <h1>{{ item.flight_status }}</h1>

            </div>

            <div class="card_trip">

                <div class="trip_from">

                    <h1>{{ item.departure_iata }}</h1>
                    <h2>{{ item.departure_airport }}</h2>

                </div>

                <div class="trip_icon">

                    <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/553328/From.png"/>

                </div>

                <div class="trip_to">

                    <h1>{{ item.arrival_iata }}</h1>
                    <h2>{{ item.arrival_airport }}</h2>

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

                    <h3>{{ item.airline_name }}</h3>

                </div>

                <div class="seating_seat">

                    <h2>Aircraft</h2>
                    <h3>{{ item.aircraft_registration }}</h3>

                </div>

            </div>

            <div class="card_details">

                <div class="details_flight">

                    <h2>Flight Number</h2>

                    <h3>{{ item.flight_number }}</h3>

                </div>

                <div class="details_date">

                    <h2>Flight IATA</h2>

                    <h3>{{ item.flight_iata }}</h3>

                </div>

                <div class="details_time">

                    <h2>Flight ICAO</h2>

                    <h3>{{ item.flight_icao }}</h3>

                </div>

            </div>

        </div>

    </div>

</template>

<script>

    import {bus} from '../main'

    export default {
        data: () => ({
            data: null,
        }),
        created() {
            bus.$on('data', (data) => {
                this.data = data
                console.log(this.data)
            })
        }
    }
</script>

<style>
    @import '../assets/styles/search.css';
</style>