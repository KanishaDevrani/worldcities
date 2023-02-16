<template>
  <img alt="Vue logo" src="./assets/worldimage.png">
  <p><b>Cities of the World</b></p>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <table class="table table-bordered table-responsive">
          <thead class="bg-secondary">
            <tr>
              <th class="col-6">Country | Geo Name Id | Name | Sub Country</th>
              <th class="col-6">Data</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item,index) in items" :key="index">
            <td class="col-6">{{ item.country }} | {{ item.geonameid }} | {{ item.name }} | {{ item.subcountry }}</td>
            <td class="col-6 text-start">
              <p>01 There are more than 50,000 cities in the world.</p>
              <p>02 Megacities are cities with more than 10 million people living in them.</p>
              <p>03 Tokyo is the most populated city in the world, with more than 38 million people.</p>
              <p>04 New York is the biggest city in the world, with 8,683 km² in area.</p>
              <p>05 The Vatican City is the smallest city in the world, with only 44 hectares in area.</p>
            </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
  <div>
    <div class="row mt-3">
      <div class="col-md-12 text-center">
        <button @click="loadItems" class="btn btn-md btn-dark">Load More</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'WorldCitiesApp',
  data() {
    return {
      items: [],
      startIndex: 20,
      users: []
    };
  },
  methods: {
    loadAllItems(){
      axios.get('https://pkgstore.datahub.io/core/world-cities/world-cities_json/data/5b3dd46ad10990bca47b04b4739a02ba/world-cities_json.json')
      .then(response => {
      this.items = response.data;
      })
      .catch(error => {
        console.log(error)
      })

    },
    loadFirstItems(){
      axios.get('https://pkgstore.datahub.io/core/world-cities/world-cities_json/data/5b3dd46ad10990bca47b04b4739a02ba/world-cities_json.json')
      .then(response => {
      this.items = response.data.slice(0,10);
      })
      .catch(error => {
        console.log(error)
      })

    },
    loadItems() {
      axios.get('https://pkgstore.datahub.io/core/world-cities/world-cities_json/data/5b3dd46ad10990bca47b04b4739a02ba/world-cities_json.json')
      .then(response => {
      this.users = response.data;
      this.items=this.users.slice(0,this.startIndex);
      this.startIndex += 10;
      })
      .catch(error => {
        console.log(error)
      })
    },
  },
  mounted() {
  this.loadFirstItems();
},
}

</script>

<style>
#worldcitiesapp {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>