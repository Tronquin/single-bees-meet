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
          <p>This is a Dating site for bees and flowers of all sorts, meet your honey right now!</p>
          <a v-scroll-to="'#whatAreYou'" href="#" class="btn-GameCardsStack">Start Dating</a>
        </div>
        <div class="slides-container">
          <div class="slides">
            <div class="slides-1" />
            <div class="slides-2" />
            <div class="slides-3" />
            <div class="slides-4" />
          </div>
        </div>
      </section>
      <section id="whatAreYou" class="wrapper-whatAreYou">
        <WhatAreYou @handleSelection="handleSelection" />
      </section>
      <section v-if="(bee || flower)" id="cardStack" class="wrapper-GameCardsStack">
        <GameCardsStack
          :cards="cards"
          :bee="bee"
          :flower="flower"
          @cardAccepted="handleCardAccepted"
          @cardRejected="handleCardRejected"
          @cardSkipped="handleCardSkipped"
        />
      </section>
    </div>
    <Footer />
  </div>
</template>

<script>
import FontFaceObserver from 'fontfaceobserver'
import Navbar from '../layouts/navbar'
import Footer from '../layouts/footer'
import WhatAreYou from '../components/WhatAreYou'
import GameCardsStack from '../components/GameCardsStack'

export default {
  name: 'Index',
  components: {
    Navbar,
    WhatAreYou,
    GameCardsStack,
    Footer
  },
  data() {
    return {
      cards: [],
      onViewport: false,
      bee: false,
      flower: false,
      beeCards: [],
      flowerCards: []
    }
  },
  created() {
    const bees = {
      honey: {
        name: 'Honey',
        status: 'IN DANGER',
        info:
          'One of the most common social insects on the planet, honey bees create colonies that can be as large as 80,000 individual insects, live in hives and create honey.',
        location: 'Somewhere',
        description: 'One of the most common social insects on the planet',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-1.jpg'
      },
      bumble: {
        name: 'Bumble',
        status: 'IN DANGER',
        info:
          'Bumble bees are very large, black and yellow, bees that you see flying around your garden during the warmer months.',
        description: 'Bumble bees are very large, black and yellow',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-2.jpg'
      },
      leaf: {
        name: 'Leafcutter',
        status: 'IN DANGER',
        info:
          'These bees are about 7 to 18mm in length and look like they are made from some light metal or are very dark in color.',
        description:
          'hese bees are about 7 to 18mm in length and look like they are made from some light metal ',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-3.jpg'
      },
      carpen: {
        name: 'Carpenter',
        status: 'IN DANGER',
        info:
          'Carpenter bees are tricky to spot, but you may see them flying around you if you are near their chosen nesting area.',
        description: 'Carpenter bees are tricky to spot',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-4.jpg'
      },
      mining: {
        name: 'Mining',
        status: 'IN DANGER',
        info:
          'There’s about 1,200 species of bees in the Andrena family, most commonly called mining bees. They are very similar in their behavior as digger bees.',
        description:
          'There’s about 1,200 species of bees in the Andrena family',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-5.jpg'
      },
      plaste: {
        name: 'Plasterer',
        status: 'IN DANGER',
        info:
          'Plasterer bees are a little bigger than sweat bees, coming in around 10 – 18mm in length and also quite hairy-looking.',
        description: 'Plasterer bees are a little bigger than sweat bees',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-6.jpg'
      }
    }
    const flowers = {
      Sunflower: {
        name: 'Sunflower',
        status: 'IN NEED OF BEES',
        info:
          'Sunflowers are tall with big, prolific heads that contain smaller flowers inside the circular disc. It’s basically a nectar and pollen playground for pollinators, but we also benefit from the crop because it yields seeds and oil.',
        location: 'somewhere',
        description:
          'Sunflowers are tall with big, prolific heads that contain smaller flowers inside the circular disc.',
        show: true,
        showMoreInfo: false,
        img: 'sunflower.jpg'
      },
      Lilacs: {
        name: 'Lilacs',
        status: 'IN NEED OF BEES',
        info:
          'Lilacs come in seven colors and are easy to grow. Most shrubs grow at eye-level and give off a sweet, floral fragrance to keep the bees and butterflies coming back for more.',
        location: 'somewhere',
        description: 'Lilacs come in seven colors and are easy to grow',
        show: true,
        showMoreInfo: false,
        img: 'lilacs.jpg'
      },
      Lavander: {
        name: 'Lavander',
        status: 'IN NEED OF BEES',
        info:
          'Lavender plants are much-buzzed about when it comes to honey bees—possibly because of their long bloom time and the fact that they’re rich in nectar.',
        location: 'somewhere',
        description:
          'Lavender plants are much-buzzed about when it comes to honey bees',
        show: true,
        showMoreInfo: false,
        img: 'lavander.jpg'
      },
      Wisteria: {
        name: 'Wisteria',
        status: 'IN NEED OF BEES',
        info:
          'Wisteria vines are quite fragrant, and when blossoms start to bloom during its short growing season, you can expect to see a swarm buzzing around this charming climber.',
        location: 'somewhere',
        description: 'Wisteria vines are quite fragrant',
        show: true,
        showMoreInfo: false,
        img: 'wisteria.jpg'
      },
      Mint: {
        name: 'Mint',
        status: 'IN NEED OF BEES',
        info:
          'When it’s hot outside, Southerners will find any excuse to sneak a little mint in their cocktails, main dishes, and desserts. So it should come as no surprise that bees love the plant too, especially water mint.',
        location: 'somewhere',
        description:
          'When it’s hot outside, Southerners will find any excuse to sneak a little mint in their cocktails.',
        show: true,
        showMoreInfo: false,
        img: 'mint.jpg'
      },
      Poppies: {
        name: 'Poppies',
        status: 'IN NEED OF BEES',
        info:
          'This showy spring flower provides a banquet of food or pollen, where honey bees often frequent the plant’s flowering buffet',
        location: 'somewhere',
        description:
          'This showy spring flower provides a banquet of food or pollen.',
        show: true,
        showMoreInfo: false,
        img: 'poppies.jpg'
      }
    }
    for (const key in bees) {
      if (bees.hasOwnProperty(key)) {
        this.beeCards.push(bees[key])
      }
    }
    for (const key in flowers) {
      if (flowers.hasOwnProperty(key)) {
        this.flowerCards.push(flowers[key])
      }
    }
  },
  mounted() {
    // Font Loader
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
        SourceSansLight.load()
        SourceSansBold.load()
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
        PlayfairDisplayBold.load()
      })
      .catch(function () {
        html.classList.remove('fonts-loading')
        html.classList.add('fonts-failed')
        sessionStorage.fontsLoaded = false
      })

    if (sessionStorage.fontsLoaded) {
      html.classList.add('fonts-loaded')
    }
  },
  methods: {
    handleSelection(bee, flower) {
      if (bee) {
        this.bee = bee
        this.cards = this.beeCards
      }

      if (flower) {
        this.flower = flower
        this.cards = this.flowerCards
      }
    },
    handleCardAccepted() {
      console.log('handleCardAccepted')
    },
    handleCardRejected() {
      console.log('handleCardRejected')
    },
    handleCardSkipped() {
      console.log('handleCardSkipped')
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~/assets/scss/main.scss";
section {
  height: 100vh;
}
.wrapper {
  &-landing {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 0;
    grid-template-areas: "headline image" "headline image";
    padding: 2.5em 0;
    .left-side-container {
      grid-area: headline;
      display: flex;
      flex-flow: column wrap;
      h1 {
        font-family: "PlayfairDisplayBold";
        font-size: 7.5em;
        letter-spacing: 10px;
        color: $sunflower-black;
        text-transform: uppercase;
      }
      p {
        margin-top: 1.5em;
        font-family: "SourceSansLight";
        font-size: 2em;
        color: $sunflower-black;
        width: 80%;
      }
      .btn-GameCardsStack {
        text-decoration: none;
        text-align: center;
        margin-top: 3em;
        width: 50%;
        padding: 1em;
        border-radius: 50px;
        background-color: $sunflower-blue;
        border: none;
        outline: none;
        font-family: "SourceSansBold";
        font-size: 1.2em;
        cursor: pointer;
        color: $sunflower-black;
        text-transform: uppercase;
        transition: 0.2s background-color ease-in-out;
        &:hover {
          background-color: $sunflower-orange;
        }
      }
    }
    .slides-container {
      height: 80%;
      grid-area: image;
      background-color: $sunflower-blue;
      .slides {
        position: relative;
        width: 100%;
        height: 100%;
        border-radius: 50px;
        background-color: transparent;
        &-1,
        &-2,
        &-3,
        &-4 {
          position: absolute;
          width: 100%;
          height: 100%;
        }

        &-1 {
          background: url("../static/img/bee-draw-01.png") no-repeat center;
          animation: fade 8s infinite ease-in-out;
        }

        &-2 {
          background: url("../static/img/bee-draw-02.png") no-repeat center;
          background-size: 80%;
          animation: fade2 8s infinite ease-in-out;
        }

        &-3 {
          background: url("../static/img/bee-draw-03.png") no-repeat center;
          background-size: cover;
          animation: fade3 8s infinite ease-in-out;
        }

        &-4 {
          background: url("../static/img/bee-draw-04.png") no-repeat center;
          background-size: cover;
          animation: fade4 8s infinite ease-in-out;
        }
        @keyframes fade {
          0% {
            opacity: 1;
          }
          25% {
            opacity: 0;
          }
          50% {
            opacity: 0;
          }
          75% {
            opacity: 0;
          }
          100% {
            opacity: 1;
          }
        }
        @keyframes fade2 {
          0% {
            opacity: 0;
          }
          25% {
            opacity: 1;
          }
          50% {
            opacity: 0;
          }
          75% {
            opacity: 0;
          }
          100% {
            opacity: 0;
          }
        }
        @keyframes fade3 {
          0% {
            opacity: 0;
          }
          25% {
            opacity: 0;
          }
          50% {
            opacity: 1;
          }
          75% {
            opacity: 0;
          }
          100% {
            opacity: 0;
          }
        }
        @keyframes fade4 {
          0% {
            opacity: 0;
          }
          25% {
            opacity: 0;
          }
          50% {
            opacity: 0;
          }
          75% {
            opacity: 1;
          }
          100% {
            opacity: 0;
          }
        }
      }
    }
  }
  &-whatAreYou {
    display: flex;
    flex-flow: column wrap;
    justify-content: center;
    align-items: center;
  }
  &-GameCardsStack {
    position: relative;
  }
}

@include mq-tablet {
  .wrapper {
    max-width: 960px;
    &-landing {
      display: flex;
      flex-flow: column wrap;
      justify-content: center;
      align-items: center;
      .slides-container {
        display: none;
      }
    }
  }
}
@include mq-tablet {
}
</style>
