<template>
  <Header :theme="theme" :title="title" @toggle-theme="toggleTheme" />
  <CountryGrid :theme="theme" :countries="countries" @show-modal="countryCCN3 => showModal(countryCCN3)" />
  <Modal :theme="theme" :country="country" :modal-active="modalActive" @hide-modal="hideModal" />
</template>

<script>
import axios from 'axios'
import Header from './components/Header.vue'
import CountryGrid from './components/CountryGrid.vue'
import Modal from './components/Modal.vue'

console.log(axios)

export default {
  name: 'App',
  components: {Header, CountryGrid, Modal},
  data() {
    return {
      title: 'Countries',
      theme: 'light',
      loading: true,
      errored: false,
      countries: null,
      country: {},
      modalActive: false
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
    fetchCountries() {
      const url = 'https://restcountries.com/v3.1/all'
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
    padding: $gtr-hlf $gtr;
    border-radius: 23px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 0 $gtr;
    transition: color $tr-default, background-color $tr-default;
    &:hover {
      cursor: pointer;
    }
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
    line-height: 1;
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
