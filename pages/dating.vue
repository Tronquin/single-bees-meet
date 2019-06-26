<template>
  <div class="wrapper">
    <Navbar />
    <div class="wrapper-dating">
      <section id="whatAreYou" class="wrapper-dating-whatAreYou">
        <WhatAreYou @handleSelection="handleSelection" />
      </section>
      <section v-if="(bee || flower)" id="cardStack" class="wrapper-dating-GameCardsStack">
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
import Navbar from '../layouts/navbar'
import Footer from '../layouts/footer'
import WhatAreYou from '../components/WhatAreYou'
import GameCardsStack from '../components/GameCardsStack'
export default {
  name: 'Dating',
  components: {
    Navbar,
    Footer,
    WhatAreYou,
    GameCardsStack
  },
  data() {
    return {
      cards: [],
      beeCards: [],
      flowerCards: [],
      bee: false,
      flower: false
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

<style lang="scss">
.tutorial {
  display: none !important;
}
</style>
