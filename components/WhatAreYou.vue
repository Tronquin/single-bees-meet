<template>
  <div class="whatAreYou">
    <h2>What Are You?</h2>
    <div class="choice-container">
      <div class="option grow" @click.once="OptionSelected(ImBee, ImFlower = true)" v-scroll-to="'#cardStack'">
        <div class="hexagon-orange">
          <img v-lazy="`img/${bee}`" alt="bee.choice" class="bee">
        </div>
      </div>
      <div class="option grow" @click.once="OptionSelected(ImBee = true, ImFlower)" v-scroll-to="'#cardStack'">
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
      this.ImBee = ImBee
      this.ImFlower = ImFlower
      this.$emit('handleSelection', this.ImBee, this.ImFlower)
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";
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
</style>
