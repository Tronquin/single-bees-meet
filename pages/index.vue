<template>
  <div class="index">
    <Navbar />
    <div class="wrapper">
      <section class="wrapper-landing">
        <div class="left-side-container">
          <h1>
            Wanna
            <br>Polli
            <br>nate?
          </h1>
          <p>This is a dating site for bees and flowers of all sorts, meet your honey right now!</p>
          <button class="btn-dating">
            Start Dating
          </button>
        </div>
        <div class="slides-container">
          <div class="slides">
            <div class="slides-1" />
            <div class="slides-2" />
            <div class="slides-3" />
          </div>
        </div>
      </section>
      <Facts />
      <section class="wrapper-whatAreYou">
        <WhatAreYou />
      </section>
      <Facts />
      <section class="wrapper-dating">
        <Dating />
      </section>
      <Facts />
      <section class="wrapper-match">
        <Match />
      </section>
    </div>
    <Footer />
  </div>
</template>

<script>
import FontFaceObserver from 'fontfaceobserver'
import Navbar from '../layouts/navbar'
import WhatAreYou from '../components/WhatAreYou'
import Dating from '../components/Dating'
import Match from '../components/Match'
import Facts from '../components/Facts'
import Footer from '../layouts/footer'

export default {
  name: 'Index',
  components: {
    Navbar,
    WhatAreYou,
    Dating,
    Match,
    Facts,
    Footer
  },
  mounted() {
    const PlayfairDisplay = new FontFaceObserver('PlayfairDisplay')
    const SourceSans = new FontFaceObserver('SourceSans')
    const PlayfairDisplayBold = new FontFaceObserver('PlayfairDisplayBold')
    const SourceSansLight = new FontFaceObserver('SourceSansLight')
    const SourceSansBold = new FontFaceObserver('SourceSansBold')
    const html = document.documentElement
    SourceSans.load()
      .then(function () {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-loaded')
        sessionStorage.fontsLoaded = true
        console.log('SourceSans has loaded.')
        SourceSansLight.load().then(() => {
          console.log('SourceSansLight Has Loaded')
        })
        SourceSansBold.load().then(() => {
          console.log('SourceSansBold Has Loaded')
        })
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
        PlayfairDisplayBold.load().then(() => {
          console.log('PlayfairDisplayBold has loaded')
        })
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
    margin: 2em 0;
    height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 0;
    grid-template-areas: "headline image" "headline image";
    .left-side-container {
      grid-area: headline;
      display: flex;
      flex-flow: column wrap;
      justify-content: space-around;
        h1 {
          font-family: "PlayfairDisplayBold";
          font-size: 7.5em;
          letter-spacing: 10px;
          color: $sunflower-black;
          text-transform: uppercase;
        }
        p {
          font-family: "SourceSansLight";
          font-size: 2em;
          color: $sunflower-black;
          width: 65%;
        }
        .btn-dating {
          width: 50%;
          padding: 1em;
          border-radius: 50px;
          background-color: $sunflower-blue;
          border: none;
          outline: none;
          font-family: 'SourceSansBold';
          font-size: 1.2em;
          cursor: pointer;
        }
    }
    .slides-container {
        grid-area: image;
        background-color: $sunflower-blue;
      .slides {
        position: relative;
        width: 100%;
        height: 100%;
        border-radius: 50px;
        background-color: transparent;
        &-1,&-2,&-3 {
          position: absolute;
          width: 100%;
          height: 100%;
        }

        &-1 {
          background: url('../assets/images/main-bee.png') no-repeat center;
          animation: fade 8s infinite ease-in-out;
        }

        &-2 {
          background: url('../assets/images/main-sunflower.png') no-repeat center;
          background-size: 80%;
          animation: fade2 8s infinite ease-in-out;
        }

        &-3 {
          background: url('../assets/images/wory-bee.png') no-repeat center;
          background-size: cover;
          animation: fade3 8s infinite ease-in-out;
        }
        @keyframes fade
        {
          0%   {opacity:1}
          33.333% { opacity: 0}
          66.666% { opacity: 0}
          100% { opacity: 1}
        }
        @keyframes fade2
        {
          0%   {opacity:0}
          33.333% { opacity: 1}
          66.666% { opacity: 0 }
          100% { opacity: 0}
        }
        @keyframes fade3
        {
          0%   {opacity:0}
          33.333% { opacity: 0}
          66.666% { opacity: 1}
          100% { opacity: 0}
        }
      }
    }

  }
}

@include for-tablet-landscape-up {
}
</style>
