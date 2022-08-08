<template>
  <Header :theme="theme" :title="title" @change="toggleTheme" />
  <CountryGrid :theme="theme" />
  <Modal :theme="theme" />
</template>

<script>
import Header from './components/Header.vue'
import CountryGrid from './components/CountryGrid.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {Header, CountryGrid, Modal},
  data() {
    return {
      title: 'Countries Explorer',
      theme: 'light'
    }
  },
  methods: {
    toggleTheme() {
      this.theme === 'light' ? this.theme = 'dark' : this.theme = 'light'
      console.log(this.theme)
    }
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
