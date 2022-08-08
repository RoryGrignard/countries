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
      title: 'Countries',
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #000000;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

#app * {
  box-sizing: border-box;
}

.dark * {
  color: #fff;
}

body {
  margin: 0;
}
</style>
