<template>
  <div class="index">
    <Navbar></Navbar>
    <section class="section-index">
      <h1>BEES ARE COOL!</h1>
    </section>
  </div>
</template>

<script>
import FontFaceObserver from 'fontfaceobserver'
import Navbar from '../layouts/navbar'
export default {
  name: 'Index',
  components: {
    Navbar
  },
  mounted() {
    const Archivo = new FontFaceObserver('Archivo')
    const PlayfairDisplay = new FontFaceObserver('PlayfairDisplay')
    const html = document.documentElement
    Archivo.load()
      .then(function() {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-loaded')
        sessionStorage.fontsLoaded = true
        console.log('Archivo has loaded.')
      })
      .catch(function() {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-failed')
        sessionStorage.fontsLoaded = false
      })

    PlayfairDisplay.load()
      .then(function() {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-loaded')
        sessionStorage.fontsLoaded = true
        console.log('PlayfairDisplay has loaded.')
      })
      .catch(function() {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-failed')
        sessionStorage.fontsLoaded = false
      })

    if (sessionStorage.fontsLoaded) {
      html.classList.add('fonts-loaded')
    }
  }
}
</script>

<style lang="scss">
.section-index {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: black;
  color: pink;
  h1 {
    font-family: 'PlayfairDisplay';
    font-size: 5em;
  }
}
</style>
