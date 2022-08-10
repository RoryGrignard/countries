<template>
  <Header :theme="theme" :title="title" @toggle-theme="toggleTheme" />
  <Filter :theme="theme" @filter-region="region => filterRegion(region)" @search-query="searchQuery => searchCountry(searchQuery)" @reset-filters="resetFilters" />
  <Grid :theme="theme" :countries="countries" @show-modal="countryCCN3 => showModal(countryCCN3)" />
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

console.log(axios)

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
    }
  },
  methods: {
    showModal(countryCCN3) {
      let selectedCountry = this.countries.filter(country => country.ccn3 == countryCCN3)
      this.country = selectedCountry
      this.modalActive = true
    },
    hideModal() {
      this.modalActive = false
      this.country = {}
    },
    toggleTheme() {
      this.theme === 'light' ? this.theme = 'dark' : this.theme = 'light'
    },
    resetFilters() {
      this.search = null
      this.region = null
      this.countries = null
      this.fetchCountries()
    },
    searchCountry(searchQuery) {
      this.search = searchQuery
      this.region = null
      this.countries = null
      this.fetchCountries()
    },
    filterRegion(region) {
      this.search = null
      this.region = region
      this.countries = null
      this.fetchCountries()
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
}

#app * {
  box-sizing: border-box;
}

body {
  margin: 0;
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

button {
  outline: none;
  background-color: transparent;
  border: 2px solid transparent;
  padding: $gtr-hlf 18px;
  border-radius: 23px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0 $gtr;
  line-height: 1;
  transition: color $tr-default, background-color $tr-default, border-color $tr-default;
  &:hover {
    cursor: pointer;
  }
  &:focus {
    outline: none;
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

// Theme styles
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
  button {
    color: $c-dodger-blue;
    border-color: $c-dodger-blue;
    &:hover {
      background-color: $c-dodger-blue-tr-2;
    }
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
  button {
    color: $c-ocean-green;
    border-color: $c-ocean-green;
    &:hover {
      background-color: $c-ocean-green-tr-2;
    }
  }
}

</style>
