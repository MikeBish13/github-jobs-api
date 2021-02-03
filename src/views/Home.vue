<template>
  <div id="app">
      <Header />
      <SearchBar v-on:start-search="search" />
      <Jobs v-bind:jobs="jobs" />
  </div>
</template>

<script>
import Jobs from '../components/Jobs'
import SearchBar from '../components/SearchBar'
import Header from '../layout/Header.vue'

export default {
  name: 'App',
  components: {
    SearchBar,
    Jobs,
    Header
  },
data() {  
  return {
    jobs: []
  }
},
methods: {
  search(newSearch) { 
    const { title, location, fullTime } = newSearch;
    let fullTimeSearch = fullTime ? 'on' : 'off';
    fetch(`https://cors-anywhere.herokuapp.com/https://jobs.github.com/positions.json?search=${title}&full_time=${fullTimeSearch}&location=${location}`)
    .then((res) => res.json())
    .then((data) => this.jobs = data)
  }
},
created() {
  fetch('https://cors-anywhere.herokuapp.com/https://jobs.github.com/positions.json?page=1')
  .then((res) => res.json())
  .then((data) => this.jobs = data)
  .catch(err => console.log(err))
}
}
</script>

<style>

</style>