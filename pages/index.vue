<template>
  <div class="index">
    <Navbar />
    <div class="wrapper">
      <section class="wrapper-landing">
        <div class="headline">
          <h1>
            Wanna
            <br>Polli
            <br>nate?
          </h1>
          <p>This is a dating site for bees and flowers of all sorts, meet your honey right now!</p>
        </div>
        <div class="whatAreYou">
          <WhatAreYou />
        </div>
        <div class="imageSlide" />
      </section>
      <Facts />
      <section class="wrapper-resources">
        <div class="background-blue">
          <h2>We Need Help</h2>
          <img src="../assets/images/tyler's bee cropped.png" alt="bee">
          <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem.</p>
          <button>Help Us</button>
        </div>
      </section>
      <Facts />
      <section class="wrapper-about">
        <div class="background-repeat">
          <h2>Learn About Us</h2>
          <div class="background-dark">
            <p>
              Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem.
              Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic.
            </p>
          </div>
          <button>Learn More</button>
        </div>
      </section>
      <Facts />
      <section class="wrapper-contact">
        <div class="contactFormContainer">
          <ContactForm />
        </div>
        <div class="honey-container">
          <h2>Honey</h2>
          <h2>Honey</h2>
          <h2>Honey</h2>
        </div>
        <div class="sunflower">
          <img src="../assets/images/sunflower-of-pablo.png" alt="sunflower">
        </div>
      </section>
    </div>
    <Footer />
  </div>
</template>

<script>
import FontFaceObserver from 'fontfaceobserver'
import Navbar from '../layouts/navbar'
import WhatAreYou from '../components/WhatAreYou'
import Facts from '../components/Facts'
import ContactForm from '../components/ContactForm'
import Footer from '../layouts/footer'

export default {
  name: 'Index',
  components: {
    Navbar,
    WhatAreYou,
    Facts,
    ContactForm,
    Footer
  },
  mounted() {
    const PlayfairDisplay = new FontFaceObserver('PlayfairDisplay')
    const SourceSans = new FontFaceObserver('SourceSans')
    const html = document.documentElement
    SourceSans.load()
      .then(function () {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-loaded')
        sessionStorage.fontsLoaded = true
        console.log('SourceSans has loaded.')
      })
      .catch(function () {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-failed')
        sessionStorage.fontsLoaded = false
      })
    PlayfairDisplay.load()
      .then(function () {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-loaded')
        sessionStorage.fontsLoaded = true
        console.log('PlayfairDisplay has loaded.')
      })
      .catch(function () {
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
@import "~/assets/scss/main.scss";

.wrapper {
  &-landing {
    height: 90vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    grid-template-areas: "headline image" "whatAreYou image";
    .headline {
      grid-area: headline;
      h1 {
        font-family: "PlayfairDisplay";
        font-size: 8em;
        color: $sunflower-black;
        text-transform: uppercase;
      }
      p {
        font-family: "SourceSans";
        font-size: 2.5em;
        color: $sunflower-black;
        width: 65%;
      }
    }
    .whatAreYou {
      grid-area: whatAreYou;
    }
    .imageSlide {
      grid-area: image;
      width: 100%;
      height: 100%;
      background-color: $sunflower-blue;
    }
  }
}

@include for-tablet-landscape-up {
}
</style>
