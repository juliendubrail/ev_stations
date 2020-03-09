<template>
    <b-row>
        <b-col cols="12">
            <h2>
                Ev Charging 
            </h2>
            <b-table striped hover :items="stations" :fields="fields" @row-clicked="details">
                
            </b-table>
        </b-col>    
    </b-row>
</template>

<script>
import router from '../router'
import { Stations } from '../Stations'

export default {
    name: 'List',
    data (){
        return {
            fields: [
                { key: 'id'},
                { key: 'name', label: 'City', class: 'text-left', thClass: 'text-center'},
                { key: 'location', label: 'Location', class: 'text-left', thClass: 'text-center'}
            ],
            teams: Stations,
            errors: []
        }
    },
    created () {
        this.stations = Stations
    },
    methods: {
        details (station) {
            router.push({ name: 'Details', params: {id: station.id}})
        }
    }
    
}
</script>

<style>
.table {
    width: 96%;
    margin: 0 auto;
}
</style>