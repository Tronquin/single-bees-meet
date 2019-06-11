<template>
  <div class="whatAreYou">
    <h2>What Are You?</h2>
    <div class="choice-container">
      <div class="option">
        <div class="hexagon" />
        <img src="../assets/images/main-bee.png" alt="bee.choice" class="bee">
      </div>
      <div class="option">
        <div class="hexagon" />
        <img src="../assets/images/main-sunflower.png" alt="sunflower.choice" class="flower">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'WhatAreYou'
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
    margin-top: 2.5em;
    display: flex;
    justify-content: space-between;
    align-items: center;
    .hexagon {
      position: relative;
      width: 450px;
      height: 259.81px;
      background-color: $sunflower-orange;
      margin: 129.9px 0;
    }

    .hexagon:before,
    .hexagon:after {
      content: "";
      position: absolute;
      width: 0;
      border-left: 225px solid transparent;
      border-right: 225px solid transparent;
    }

    .hexagon:before {
      bottom: 100%;
      border-bottom: 129.9px solid $sunflower-orange;
    }

    .hexagon:after {
      top: 100%;
      width: 0;
      border-top: 129.9px solid $sunflower-orange;
    }
    .bee {
      position: absolute;
    }
    .flower {
      width: 25em;
      position: absolute;
    }
  }
}
</style>
