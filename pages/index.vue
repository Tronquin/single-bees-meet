<template>
  <div class="index">
    <Navbar />
    <div class="wrapper">
      <section class="section-index">
        <div class="text-container">
          <img src="../assets/images/sunflower-of-pablo.png" alt="Sunflower of Pablo" class="image-of-pablo">
          <h2 class="pollinate-repeat">
            Wanna <span>Pollinate?</span>
          </h2>
          <h2 class="pollinate-repeat">
            Wanna Pollinate?
          </h2>
          <h2 class="pollinate-repeat">
            Wanna Pollinate?
          </h2>
          <h2 class="pollinate-repeat">
            Wanna Pollinate?
          </h2>
          <h2 class="pollinate-repeat">
            Wanna Pollinate?
          </h2>
          <h2 class="pollinate-repeat">
            Wanna Pollinate?
          </h2>
          <h2 class="pollinate-repeat">
            Wanna Pollinate?
          </h2>
        </div>
        <div class="learn-more">
          <p>          Single Bees Meet Buzz is a Dating site where Bees and Flowers can find their honey!</p>
          <p>Wanna Learn More? <br> Click Here</p>
        </div>
      </section>
      <Facts />
      <section class="section-dating">
        <ImageSlider />
        <WhatAreYou />
        <div class="text-container">
          <h3>Why did the bee got married?</h3>
          <h4>Because He/She found His/Her Honey</h4>
          <button class="dating-btn" />
        </div>
      </section>
      <section class="section-resources">
        <div class="text-container">
          <h3>Honey</h3>
          <h3>Honey</h3>
          <h3>Honey</h3>
        </div>
        <div class="resources-container">
          <h2>There a millions of articles and resources about Bees!</h2>
          <h3>And you should definitively read them</h3>
          <Resources />
        </div>
      </section>
      <section class="section-contact">
        <h3 class="contact-headline">
          Wanna Know More?
        </h3>
        <ContactForm />
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
import ImageSlider from '../components/ImageSlider'
import Resources from '../components/Resources'
import ContactForm from '../components/ContactForm'
import Footer from '../layouts/footer'

export default {
  name: 'Index',
  components: {
    Navbar, WhatAreYou, Facts, ImageSlider, Resources, ContactForm, Footer
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
.section-index {
  position: relative;
  background-image: url('../assets/images/tyler\'s bee cropped.png');
  background-size: 200px;
  background-repeat: space;
  height: 100vh;
  display: flex;
  flex-flow: row wrap;
  justify-content: space-between;
  align-items: center;
  .text-container {
    position: relative;
    .image-of-pablo {
      width: 50%;
      position: absolute;
      left: 75px;
      bottom: 0;
      transform: rotate(-20deg);
    }
    .pollinate-repeat {
      font-family: "PlayfairDisplay";
      font-size: 3.8em;
      color: white;
      letter-spacing: 4px;
      text-transform: uppercase;
      span {
        margin-left: 1em;
      }
    }
  }

  .tylersBee {
    margin-top: auto;
    margin-bottom: 5em;
  }

  .learn-more {
    background: black;
    padding: 0.5em;
    font-family: "PlayfairDisplay";
    position: absolute;
    width: 40%;
    height: 9em;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-flow: column wrap;
    color: white;
    right: 0;
    bottom: 3em;
    font-size: 2em;
    text-align: center;
    cursor: pointer;
    p{
      margin-bottom: 0.5em;
    }

    &:hover {
      color: $sunflower-yellow-dark;
    }
  }
}
@include for-tablet-landscape-up {
    .section-index {
      flex-flow: column-reverse wrap;
      justify-content: space-around;
      .pollinate-repeat {
        font-size: 3em;
      }

      .text-container {
        text-align: center;
        h3 {
          font-size: 1em;
        }
      }
    }
}
</style>
