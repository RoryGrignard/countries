<template>
  <Header :theme="theme" :title="title" @change="toggleTheme" />
  <CountryGrid :theme="theme" :countries="countries" />
  <Modal :theme="theme" />
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
      showCountry: false
    }
  },
  methods: {
    toggleTheme() {
      this.theme === 'light' ? this.theme = 'dark' : this.theme = 'light'
    },
    fetchCountries() {
      const url = 'https://restcountries.com/v3.1/all'
      axios
      .get(url)
      .then(response => {
        console.log(response)
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

*[class*="__container"] {
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
  label,
  input,
  textarea,
  select,
  button {
    transition: color $trans-default;
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
  label,
  input,
  textarea,
  select,
  button {
    font-family: 'Roboto', sans-serif;
  }

// Theme styles
.light {
  h1,
  h2,
  h3,
  h4,
  h5,
  h6,
  p {
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
  p {
    color: $c-white;
  }
}

</style>
