<template>
  <img src="./assets/transistor-delivery.png" />
  <urlShortenerApp />
  <Footer />
</template>

<script>
import urlShortenerApp from './components/UrlShortener.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    urlShortenerApp,
    Footer
  }
}
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  body {
    background-color: #FEFBE9;
  }

  img {
    height: 30%;
    width: 30%;
    display: block;
    margin: 0 auto;
  }

  @media only screen and (max-width: 1024px) {
    img {
      height: 75%;
      width: 75%;
    }
  }

  @media only screen and (max-width: 500px) {
    img {
      height: 75%;
      width: 75%;
    }
  }
</style>

