<template>
  <b-row>
    <b-col cols="12">
      <h2>
        EV charging Station {{team.location}}
      </h2>
      <b-jumbotron>
    <template v-slot:header>{{team.name}}</template>

    <template v-slot:lead>
          <b-img src="https://picsum.photos/1024/400/?image=41" fluid alt="Responsive image"></b-img>
          <br>
          percentage remaining: {{team.percentRemaining}}<br>
          range: {{team.range}}<br>
    </template>

    <hr class="my-4">

    <b-button block class="maps-btn" variant="success" @click="showMap(team.lat,team.lng)">Show Location</b-button>
  </b-jumbotron>
    </b-col>
  </b-row>
</template>

<script>

import router from '../router'
import { Team } from '../Team'

export default {
  name: 'Details',
  data () {
    return {
      key: '',
      teams: Team,
      team: {}
    }
  },
  created () {
    const id = parseInt(this.$route.params.id, 0)
    this.team = this.teams.find(x => x.id === id)
  },
  methods: {
    showMap(lat, lng){
      router.push({name: 'Example', params: {lat: lat, lng: lng}})
    }
  } 
}
</script>

<style>
  .jumbotron {
    padding: 2rem;
  }
  .maps-btn {
    margin-right: 20px;
    width: 70px;
  }
</style>