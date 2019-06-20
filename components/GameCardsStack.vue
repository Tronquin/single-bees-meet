<template>
  <div>
    <div class="tutorial">
      <div class="tutorial-left">
        <h4>Swipe <br> Left <br> to <br> Reject!</h4>
      </div>
      <div class="tutorial-right">
        <h4>Swipe <br> Right <br> to <br> Accept!</h4>
      </div>
    </div>
    <div v-if="bee" class="cards">
      <GameCard
        v-for="(card, index) in cards"
        :key="index"
        :card="card"
        :index="index+1"
        :is-current="true"
        @cardAccepted="$emit('cardAccepted');"
        @cardRejected="$emit('cardRejected');"
        @cardSkipped="$emit('cardSkipped');"
        @hideCard="$emit('hideCard');"
      />
    </div>
    <div v-if="flower" class="cards">
      <GameCard
        v-for="(card, index) in cards"
        :key="index"
        :card="card"
        :index="index+1"
        :is-current="true"
        @cardAccepted="$emit('cardAccepted');"
        @cardRejected="$emit('cardRejected');"
        @cardSkipped="$emit('cardSkipped');"
        @hideCard="$emit('hideCard');"
      />
    </div>
  </div>
</template>

<script>
import GameCard from '../components/GameCard'

export default {
  name: 'GameCardsStack',
  components: {
    GameCard
  },
  props: {
    cards: {
      type: Array,
      default: () => [],
      required: true
    },
    bee: {
      type: Boolean,
      required: true
    },
    flower: {
      type: Boolean,
      required: true
    }
  },
  mounted() {
    console.log('card stack', this.cards)
  }
}
</script>
<style lang="scss" scoped>
@import "~/assets/scss/main.scss";
  .cards {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  .tutorial {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    height: 100%;
    &-left, &-right {
      text-align: center;
      font-size: 2em;
      font-family: 'PlayfairDisplay'
    }
  }

</style>
