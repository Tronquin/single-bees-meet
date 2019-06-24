<template>
  <div class="wrapper">
    <Navbar />
    <section class="wrapper-about">
      <div class="wrapper-about-container">
        <div class="row">
          <h2 class="headline-1">
            We Need Help
          </h2>
          <img v-lazy="`img/${gas}`" alt="danger" class="danger">
        </div>
        <div class="row">
          <img v-lazy="`img/${worry}`" alt="worry" class="worry">
          <p>
            Bee numbers are falling across the world. There isn’t one single cause to blame but there are three significant threats that stand out: pesticides, the varroa mite and habitat loss.
          </p>
        </div>
        <div class="row">
          <div class="column">
            <h2 class="headline-2" style="text-align: end;">
              Why are why in danger?
            </h2>
            <div v-for="(reason, index) in reasons" :key="index" class="row reasons" :class="`reason-${index+1}`">
              <img v-lazy="`img/${reason.icon}`" :alt="`reason-${index+1}-icon`" class="reason-icon-desktop">
              <div class="column reason-text">
                <div class="row">
                  <h3 :class="`reason-${index+1}-name`">
                    {{ reason.name }}
                  </h3>
                  <img :src="`img/${reason.icon}`" :alt="`reason-${index+1}-icon`" class="reason-icon-mobile">
                </div>
                <p :class="`reason-${index+1}-description`">
                  {{ reason.description }}
                </p>
              </div>
              <a :class="`reason-${index+1}-button`" :href="reason.url"><span>{{ reason.button }}</span></a>
            </div>
          </div>
        </div>
      </div>
    </section>
    <Footer />
  </div>
</template>
<script>
import Navbar from '../layouts/navbar'
import Footer from '../layouts/footer'
export default {
  name: 'About',
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      reasons: [],
      gas: 'gas.png',
      worry: 'wory-bee.png'
    }
  },
  created() {
    const json = {
      reason1: {
        icon: 'pesticide.svg',
        name: 'Pesticide',
        description: 'In non-organic farming, pesticides such as neonicotinoids are applied to crops to kill and control pests, but they also cause considerable harm to bees and other species, blocking neural pathways in their central nervous systems, causing disorientation, inability to feed and death.',
        button: 'Learn More',
        url: 'https://en.wikipedia.org/wiki/Pesticide_toxicity_to_bees'
      },
      reason2: {
        icon: 'bacteria.svg',
        name: 'Varroa Mite',
        description: 'Honey bees also face another huge threat from the varroa mite, which attaches itself to the honey bee and sucks its blood. When the bee returns to the hive, the varroa mite can spread and bring viruses and disease with them.',
        button: 'Learn More',
        url: 'https://en.wikipedia.org/wiki/Varroa_destructor'
      },
      reason3: {
        icon: 'deforestation.svg',
        name: 'Habitat Loss',
        description: 'There is also a significant threat against bees from our changing land use. As cities grow and agriculture becomes more intensive, bees are losing the wild spaces, hedgerows and meadows where they can find flowers and food.',
        button: 'Learn More',
        url: 'https://time.com/3951339/bees-climate-change/'
      }
    }
    for (const key in json) {
      if (json.hasOwnProperty(key)) {
        this.reasons.push(json[key])
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~/assets/scss/main.scss";
.wrapper {
  &-about {
    margin: 2em 0;
    &-container {
      display: flex;
      flex-flow: column wrap;
      .row {
        display: flex;
      }
      .column {
        flex-flow: column wrap;
      }
      .reasons {
        align-items: center;
        justify-content: space-between;
        margin: 2.5em 0;
        .reason-icon-desktop {
          width: 100px;
        }
        .reason-text {
          margin: 0 2.5em;
          .reason-icon-mobile {
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
      h2 {
        font-family: 'PlayfairDisplayBold';
        text-transform: uppercase;
        font-size: 8em;
      }

      .headline-1 {
        grid-area: headline;
        width: 70%;
      }

      .danger {
        grid-area: danger;
        width: 30%;
      }

      .worry {
        grid-area: worry;
        width: 30%;
        margin: 0 4em;
      }
      p {
        font-family: 'SourceSansLight';
        font-size: 2.5em;
        grid-area: paragraph;
        width: 70%;
        margin: auto 0;
      }
    }
  }
}

@include mq-tablet {
  .wrapper {
    max-width: unset;
    padding: unset;
    margin: unset;
    &-about {
      &-container {
        .row {
          justify-content: center;
          align-items: center;
          margin: 2em 0;
        }
        h2 {
          font-size: 4em;
          text-align: center !important;
        }
        .headline-1 {
          width: unset;
        }
        .danger {
          display: none;
        }

        .reasons {
          .reason-icon-desktop {
            display: none;
          }
          .reason-text {
            .reason-icon-mobile {
              display: block;
              width: 50px;
            }
            .row {
              align-items: center;
              justify-content: center;
              h3 {
                margin-bottom: 0;
                margin-right: 1em;
              }
            }
            p {
              margin-bottom: 2em;
              text-align: center;
            }
          }
          a {
            padding: 1em 3em;
          }
          flex-flow: column wrap;
        }
      }
    }
  }

}

@include mq-mobile-small {
  .wrapper {
    &-about {
      &-container {
        .row {
          &:nth-child(2) {
            flex-flow: column wrap;
            margin: 0;
          }
        }
        p {
          text-align: center;
        }
      }
    }
  }
}
</style>
