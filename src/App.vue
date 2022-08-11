<template>
  <Header :theme="theme" :title="title" :filter-visible="filterVisible" @toggle-filter="toggleFilter" @toggle-theme="toggleTheme" />
  <Filter :theme="theme" :filter-visible="filterVisible" :filtered="filtered" @filter-region="region => filterRegion(region)" @search-query="searchQuery => searchCountry(searchQuery)" @reset-filters="resetFilters" />
  <Grid :theme="theme" :loading="loading" :countries="countries" @show-modal="countryCCN3 => showModal(countryCCN3)" />
  <Transition name="fade">
    <Modal :theme="theme" :country="country" v-if="modalActive" @hide-modal="hideModal" />
  </Transition>
</template>

<script>
import axios from 'axios'
import Header from './components/Header.vue'
import Filter from './components/Filter.vue'
import Grid from './components/Grid.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {Header, Filter, Grid, Modal},
  data() {
    return {
      title: 'Countries',
      theme: 'light',
      loading: true,
      errored: false,
      countries: null,
      country: {},
      modalActive: false,
      search: null,
      region: null,
      filtered: false,
      filterVisible: false
    }
  },
  methods: {
    showModal(countryCCN3) {
      let selectedCountry = this.countries.filter(country => country.ccn3 == countryCCN3)
      this.country = selectedCountry
      this.filterVisible = false
      this.modalActive = true
    },
    hideModal() {
      this.modalActive = false
      this.country = {}
    },
    toggleFilter() {
      this.modalActive = false
      this.filterVisible = !this.filterVisible
    },
    toggleTheme() {
      this.theme === 'light' ? this.theme = 'dark' : this.theme = 'light'
    },
    resetFilters() {
      this.search = null
      this.region = null
      this.countries = null
      this.filtered = false
      this.modalActive = false
      this.fetchCountries()
    },
    searchCountry(searchQuery) {
      this.search = searchQuery
      this.region = null
      this.countries = null
      this.modalActive = false
      this.fetchCountries()
      this.filtered = true
    },
    filterRegion(region) {
      this.search = null
      this.region = region
      this.countries = null
      this.modalActive = false
      this.fetchCountries()
      this.filtered = true
    },
    fetchCountries() {
      this.loading = true
      let url = 'https://restcountries.com/v3.1/'
      if (this.search) {
        url += 'name/' + this.search
      } else if (this.region) {
        url += 'region/' + this.region
      } else {
        url += 'all'
      }
      axios
      .get(url)
      .then(response => {
        this.countries = response.data
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loading = false)
    }
  },
  mounted() {
    this.fetchCountries()
  }
}
</script>

<style lang="scss">

  // Layout
  #app {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    position: relative;
  }

  #app * {
    box-sizing: border-box;
  }

  body {
    margin: 0;
    &::-webkit-scrollbar {
      display: none;
    }
    -ms-overflow-style: none;
    scrollbar-width: none;
  }

  *[class*="__container"]:not(.modal__container) {
    width: 100%;
    max-width: 1400px;
    padding: 0 $gtr;
    margin: 0 auto;
  }

  // Typography
  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  p,
  li,
  label,
  input,
  textarea,
  select,
  button {
    transition: color $tr-default;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  p {
    margin-top: 0;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    font-family: 'Roboto Slab', serif;
  }

  p,
  li,
  label,
  input,
  textarea,
  select,
  button {
    font-family: 'Roboto', sans-serif;
  }

  ul {
    margin: 0;
  }

  .light {
    h1,
    h2,
    h3,
    h4,
    h5,
    h6,
    p,
    li {
      color: $c-cod-grey;
    }
  }

  .dark {
    h1,
    h2,
    h3,
    h4,
    h5,
    h6,
    p,
    li {
      color: $c-white;
    }
  }

  // Buttons
  button {
    outline: none;
    background-color: transparent;
    border: 2px solid transparent;
    padding: 8.5px 10px;
    border-radius: 23px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0 $gtr-hlf;
    transition: opacity $tr-default, border-color $tr-default, color $tr-default;
    &:hover {
      cursor: pointer;
      opacity: .6;
    }
    &:focus {
      outline: none;
    }
    .light & {
      color: $c-dodger-blue;
      border-color: $c-dodger-blue;
    }
    .dark & {
      color: $c-ocean-green;
      border-color: $c-ocean-green;
    }
    @media (min-width: 576px) {
      padding: 8.5px 15px;
    }
  }

  //Icons
  .icon {
    width: $icon-size;
    height: $icon-size;
    transition: fill $tr-default;
    .light & {
      fill: $c-dodger-blue;
    }
    .dark & {
      fill: $c-ocean-green;
    }
  }

  // Forms
  input,
  select {
    &:focus-visible {
      outline: none;
      .light & {
      box-shadow: $box-shadow-light;
      }
      .dark & {
      box-shadow: $box-shadow-dark;
      }
    }
  }

  // Transitions
  .fade-enter-from,
  .fade-leave-to {
     opacity: 0; 
  }
  .fade-enter-to,
  .fade-leave-from {
      opacity: 1;
  }
  .fade-enter-active,
  .fade-leave-active {
      transition: opacity $tr-default;
  }
</style>
