<template>
  <div class="wrapper">
    <Navbar />
    <div class="wrapper-resources">
      <div class="row">
        <div class="column">
          <h2 class="headline-1">
            YOU CAN HELP US
          </h2>
          <img v-lazy="`img/${bee}`" alt="resources-bee" class="resources-bee">
        </div>
        <div class="column">
          <h3>BEE INFORMED</h3>
          <p>It’s no secret these days that bees are extremely important. In addition to being everyone’s favorite picnic guests, bees function as some of the great pollinators in the world. According to the U.S. Department of Agriculture, they feed 80 percent of the crops that we eat including broccoli, apples, asparagus, blueberries and coffee to name a few. They also pollinate alfalfa, a grass that feeds beef and dairy cows. </p>
          <div class="newspaper">
            <img v-lazy="`img/${news}`" alt="newspaper">
          </div>
          <h2 class="headline-2">
            How?
          </h2>
        </div>
      </div>
      <div class="row">
        <div class="column">
          <div v-for="(method, index) in methods" :key="index" class="methods" :class="`method-${index+1}`">
            <h4>{{ method.name }}</h4>
            <img v-lazy="`img/${method.img}`" :alt="`method-img-${index+1}`">
            <p>{{ method.description }}</p>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="column">
          <div class="row">
            <div class="column">
              <h2 class="headline-2" style="text-align: end;">
                Wanna Help Us Even More?
              </h2>
              <h3 class="headline-3">
                Donate
              </h3>
              <div v-for="(donate, index) in donations" :key="index" class="row donations" :class="`donate-${index+1}`">
                <img v-lazy="`img/${donate.icon}`" :alt="`donate-${index+1}-icon`" class="donate-icon-desktop">
                <div class="column donate-text">
                  <div class="row">
                    <h3 :class="`donate-${index+1}-name`">
                      {{ donate.name }}
                    </h3>
                    <img :src="`img/${donate.icon}`" :alt="`donate-${index+1}-icon`" class="donate-icon-mobile">
                  </div>
                  <p :class="`donate-${index+1}-description`">
                    {{ donate.description }}
                  </p>
                </div>
                <a :class="`donate-${index+1}-button`" :href="donate.url"><span>{{ donate.button }}</span></a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from '../layouts/navbar'
import Footer from '../layouts/footer'
export default {
  name: 'Resources',
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      bee: 'main-bee.png',
      news: 'newspaper.png',
      methods: [],
      donations: []
    }
  },
  created() {
    const json = {
      method1: {
        name: 'LET YOUR LAWN GET BACK TO ITS ROOTS',
        img: 'method-1.jpg',
        description: 'Put down the weed-eater! Bees don’t have any use for that perfectly manicured sea of St. Augustine. They’re over it. They prefer something similar to their natural habitat—a meadow. Think about letting a portion of your yard go back to its roots. Allow dandelions and clover to grow again (two of bees\' favorite delicacies). Not only will you spend less time mowing your lawn, the bees will thank you for it.'
      },
      method2: {
        name: 'JUST SAY NO TO PESTICIDES AND HERBICIDES',
        img: 'method-2.jpg',
        description: 'Pesticides and herbicides contain chemicals that are very harmful to bees and other beneficial insects.  Avoid chemical sprays on your plants and yard. Do some research and try some natural, bee-friendly alternatives. Even an herbicide or pesticide that labels itself as "organic" could still be a hazard. So, put down that bottle of Round Up and try some natural alternatives (and use them as sparingly as possible). And don\'t forget the soil! You can build up the dirt in your garden, clear weeds and attract the beneficial worms with something you probably have in your garage: cardboard boxes.'
      },
      method3: {
        name: 'KEEP A BEE GARDEN',
        img: 'method-3.jpg',
        description: 'You\'ve always wanted a private garden oasis, and now you have the perfect excuse to plant one. The bees need you! Plant an array of herbs and flowers that attract bees (like mint, lavender, and poppies, to name a few). Ideally, pick flowers that are native to your area and will bloom at different times of the year. Put a shallow container of water in your garden so that the bees have a place to re-hydrate and add some twigs and pebbles to give them a place to land. Make some refreshing beverages with your freshly-planted herbs and scatter patio furniture at random...for the bees.'
      },
      method4: {
        name: 'SHOP RESPONSIBLY',
        img: 'method-4.jpg',
        description: 'Supporting your local growers and supporting bees go hand in hand. When you can, buy your fruits and vegetables (and honey) from local farmers through a CSA (community supported agriculture) box or from local farmers markets. The more you can support sustainable, earth-friendly agriculture the better, but if you don\'t have access, eating organic goes a long way to help the bees!'
      }
    }
    for (const key in json) {
      if (json.hasOwnProperty(key)) {
        this.methods.push(json[key])
      }
    }

    const jsonDonations = {
      donation1: {
        icon: 'donate.svg',
        name: 'Heifer Honeybees Donation',
        description: 'A Heifer honeybee gift donation includes a bee package, hive, box and training in beekeeping techniques. When you buy bees for a family in need, your gift:Boosts income through sales of honey, wax and pollen Stimulates growth of the family’s crops through pollination Sometimes it\'s the smallest gifts that make the largest impact. Healthy beehives can double fruit and vegetable yields of small farms. Let your honeybee donation turn a family\'s struggle into a lifetime of opportunity.',
        button: 'Donate',
        url: 'https://www.heifer.org/gift-catalog/animals-nutrition/honeybees-donation.html'
      },
      donation2: {
        icon: 'donate.svg',
        name: 'Honeybee Conservancy',
        description: 'The generosity of people like you is what makes the work of our bee charity possible. Make a tax-deductible contribution to The Honeybee Conservancy (HBC) and help us build a strong network of bee advocates to curb the rapid decline of bee populations. We are grateful for your support!',
        button: 'Donate',
        url: 'https://thehoneybeeconservancy.org/donate-now/'
      },
      reason3: {
        icon: 'donate.svg',
        name: 'Pollinator',
        description: 'Thanks to people like you, our work for pollinators and P2\'s programs are made possible. You can choose to donate one-time only (BELOW) to the Pollinator Partnership or any of our programs (ABOVE) or in various ways (RIGHT). Your gift will not only benefit pollinators, it will benefit us all. Bees and other pollinators are threatened, but with your support the Pollinator Partnership is finding ways to help them. We will ensure your gift goes where it\'s needed most.',
        button: 'Donate',
        url: 'https://www.pollinator.org/donate'
      }
    }

    for (const key in jsonDonations) {
      if (jsonDonations.hasOwnProperty(key)) {
        this.donations.push(jsonDonations[key])
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~/assets/scss/main.scss";

.wrapper {
      max-width: unset;
    padding: unset;
    margin: unset;
  &-resources {
    margin: 2em 1em;
    h2 {
      font-family: 'PlayfairDisplayBold';
      text-transform: uppercase;
      font-size: 8em;
    }

    h3 {
      font-family: 'SourceSansBold';
      text-transform: uppercase;
      font-size: 4em;
      margin-bottom: 0.5em;
    }

    h4 {
      font-family: 'SourceSansBold';
      text-transform: uppercase;
      font-size: 2.5em;
      text-align: center;
    }

    p {
      font-family: 'SourceSansLight';
      font-size: 1.5em;
    }
    .headline-1 {
      margin-right: 1em;
    }

    .headline-2 {
      margin-left: auto;
    }

    .headline-3 {
      text-align: center;
      margin-top: 1em;
    }
    .row {
      display: flex;
    }

    .column {
      display: flex;
      flex-flow: column wrap;
      margin-top: 2em;
    }

    .newspaper {
      display: flex;
      img {
        margin: 0 auto;
        width: 500px;
      }
    }

    .donate-icon-desktop {
      margin: 0 4em;
    }
    .donations {
      a {
        padding: 1.5em 3em !important;
      }
    }

    .methods {
      img {
        width: 100%;
        border-radius: 50px;
        object-fit: cover;
        height: 300px;
        margin: 2em 0;
      }
      p {
        margin: 0 3.5em 2em 3.5em;
      }
    }
      .donations {
        align-items: center;
        justify-content: space-between;
        margin: 2.5em 0;
        .donate-icon-desktop {
          width: 100px;
        }
        .donate-text {
          margin: 0 2.5em;
          .donate-icon-mobile {
            display: none;
          }
          h3 {
            font-family: 'SourceSansBold';
            text-transform: uppercase;
            font-size: 2em;
            margin-bottom: 0.5em;
          }
          p {
            font-size: 1.8em;
            width: unset;
            margin: unset;
          }
        }
        a {
          text-decoration: none;
          background-color: $sunflower-blue;
          border-radius: 50px;
          font-family: 'SourceSansBold';
          color: $sunflower-black;
          padding: 0.5em 3em;
          transition: background-color ease 0.5s;
          &:hover {
            background-color: $sunflower-orange;
          }
          span {
            width: 100%;
          }
        }
      }
  }
}

@include mq-tablet {
  .wrapper {
    &-resources {
      .row {
        flex-flow: column wrap;
      }

      .headline-1 {
        text-align: center;
        margin-right: 0;
      }

      .resources-bee {
        display: none;
      }

      h3 {
        display: none;
      }

      p {
        text-align: center;
      }

      .headline-2 {
        text-align: center !important;
        margin-left: 0;
      }

      .donations {
        a {
          margin-top: 2.5em;
          padding: 1.5em 4em !important;
        }
      }
    }
  }
}

@include mq-mobile-small {
  .wrapper {
    &-resources {
      .headline-1, .headline-2 {
        font-size: 4em;
      }
      .methods {
        p {
          margin: 0;
        }
      }
      .newspaper {
        img {
          width: 100%;
        }
      }

      .donations {
        p {
          margin: 0;
        }
      }
    }
  }
}

</style>
