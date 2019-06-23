<template>
  <div class="whatAreYou">
    <h2>What Are You?</h2>
    <div class="choice-container">
      <div v-scroll-to="'#cardStack'" class="option grow" @click.once="OptionSelected(ImBee, ImFlower = true)">
        <div class="hexagon-orange">
          <img v-lazy="`img/${bee}`" alt="bee.choice" class="bee">
        </div>
      </div>
      <div v-scroll-to="'#cardStack'" class="option grow" @click.once="OptionSelected(ImBee = true, ImFlower)">
        <div class="hexagon-blue">
          <img v-lazy="`img/${flower}`" alt="sunflower.choice" class="flower">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WhatAreYou',
  data() {
    return {
      bee: 'main-bee.png',
      flower: 'main-sunflower.png',
      ImBee: false,
      ImFlower: false
    }
  },
  methods: {
    OptionSelected(ImBee, ImFlower) {
      const options = document.querySelectorAll('.option')
      options.forEach((option) => {
        option.classList.add('no-pointer')
      })
      this.ImBee = ImBee
      this.ImFlower = ImFlower
      this.$emit('handleSelection', this.ImBee, this.ImFlower)
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";
.no-pointer {
  pointer-events: none;
}
.whatAreYou {
  h2 {
    font-family: "PlayfairDisplayBold";
    font-size: 5em;
    letter-spacing: 10px;
    color: $sunflower-black;
    text-transform: uppercase;
    text-align: center;
  }
  .choice-container {
    .option {
      margin: 0 2em;
    }
    .grow { transition: all .2s ease-in-out;
    &:hover {
      transform: scale(1.1);
    }}
    margin-top: 2.5em;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .hexagon-blue {
      cursor: pointer;
      position: relative;
      width: 450px;
      height: 259.81px;
      background-color: $sunflower-blue;
      margin: 129.9px 0;
    }

    .hexagon-blue:before,
    .hexagon-blue:after {
      content: "";
      position: absolute;
      width: 0;
      border-left: 225px solid transparent;
      border-right: 225px solid transparent;
    }

    .hexagon-blue:before {
      bottom: 100%;
      border-bottom: 129.9px solid $sunflower-blue;
    }

    .hexagon-blue:after {
      top: 100%;
      width: 0;
      border-top: 129.9px solid $sunflower-blue;
    }
    .hexagon-orange {
      cursor: pointer;
      position: relative;
      width: 450px;
      height: 259.81px;
      background-color: $sunflower-orange;
      margin: 129.9px 0;
    }

    .hexagon-orange:before,
    .hexagon-orange:after {
      content: "";
      position: absolute;
      width: 0;
      border-left: 225px solid transparent;
      border-right: 225px solid transparent;
    }

    .hexagon-orange:before {
      bottom: 100%;
      border-bottom: 129.9px solid $sunflower-orange;
    }

    .hexagon-orange:after {
      top: 100%;
      width: 0;
      border-top: 129.9px solid $sunflower-orange;
    }
    .bee {
      z-index: 10;
      position: absolute;
      width: 100%;
      bottom: -20%;
    }
    .flower {
bottom: -60%;
left: 5%;
      width: 100%;
      position: absolute;
      z-index: 10;
    }
  }
}

@include mq-tablet  {
  .whatAreYou {
      margin: 3em 0;
      h2 {
        text-align: center;
      }
      .choice-container {
        flex-flow: column wrap;
        margin: 1em 0;
          .option {
            margin: 1em 0em;
        .hexagon-orange {
          position: relative;
          width: 300px;
          height: 173.21px;
          background-color: $sunflower-orange;
          margin: 86.60px 0;
        }

        .hexagon-orange:before,
        .hexagon-orange:after {
          content: "";
          position: absolute;
          width: 0;
          border-left: 150px solid transparent;
          border-right: 150px solid transparent;
        }

        .hexagon-orange:before {
          bottom: 100%;
          border-bottom: 86.60px solid $sunflower-orange;
        }

        .hexagon-orange:after {
          top: 100%;
          width: 0;
          border-top: 86.60px solid $sunflower-orange;
        }
                .hexagon-blue {
          position: relative;
          width: 300px;
          height: 173.21px;
          background-color: $sunflower-blue;
          margin: 86.60px 0;
        }

        .hexagon-blue:before,
        .hexagon-blue:after {
          content: "";
          position: absolute;
          width: 0;
          border-left: 150px solid transparent;
          border-right: 150px solid transparent;
        }

        .hexagon-blue:before {
          bottom: 100%;
          border-bottom: 86.60px solid $sunflower-blue;
        }

        .hexagon-blue:after {
          top: 100%;
          width: 0;
          border-top: 86.60px solid $sunflower-blue;
        }
      }
    }
  }
}

@include mq-mobile-small {
  .whatAreYou {
    h2 {
      font-size: 3em;
    }
    .choice-container {
      .option {
        .hexagon-orange {
          position: relative;
          width: 200px;
          height: 115.47px;
          background-color: $sunflower-orange;
          margin: 57.74px 0;
        }

        .hexagon-orange:before,
        .hexagon-orange:after {
          content: "";
          position: absolute;
          width: 0;
          border-left: 100px solid transparent;
          border-right: 100px solid transparent;
        }

        .hexagon-orange:before {
          bottom: 100%;
          border-bottom: 57.74px solid $sunflower-orange;
        }

        .hexagon-orange:after {
          top: 100%;
          width: 0;
          border-top: 57.74px solid $sunflower-orange;
        }
        .hexagon-blue {
          position: relative;
          width: 200px;
          height: 115.47px;
          background-color: $sunflower-blue;
          margin: 57.74px 0;
        }

        .hexagon-blue:before,
        .hexagon-blue:after {
          content: "";
          position: absolute;
          width: 0;
          border-left: 100px solid transparent;
          border-right: 100px solid transparent;
        }

        .hexagon-blue:before {
          bottom: 100%;
          border-bottom: 57.74px solid $sunflower-blue;
        }

        .hexagon-blue:after {
          top: 100%;
          width: 0;
          border-top: 57.74px solid $sunflower-blue;
        }
      }
    }
  }
}
</style>
