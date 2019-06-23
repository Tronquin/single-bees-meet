<template>
  <div>
    <div class="tutorial">
      <div class="tutorial-left">
        <h4>Swipe <br> Left <br> to <br> Reject!</h4>
      </div>
      <div class="tutorial-right">
        <h4>Swipe <br> Right <br> to <br> Like!</h4>
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
        @cardPicked="handlePickedCard"
      />
      <div class="noMore">
        <h3>No More Canidates?</h3>
        <h4>That's a shame! <br> But you can always learn more</h4>
        <nuxt-link to="/About" class="btn-about">
          Learn More!
        </nuxt-link>
      </div>
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
        @cardPicked="handlePickedCard"
      />
      <div class="noMore">
        <h3>No More Canidates?</h3>
        <h4>That's a shame! <br> But you can always learn more</h4>
        <nuxt-link to="/About" class="btn-about">
          Learn More!
        </nuxt-link>
      </div>
    </div>

    <ModalMatch
      v-show="isModalVisible"
      :card="pickedCard"
      @close="closeModal"
    />
  </div>
</template>

<script>
import GameCard from '../components/GameCard'
import ModalMatch from '../components/Match'

export default {
  name: 'GameCardsStack',
  components: {
    GameCard,
    ModalMatch
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
  data() {
    return {
      delta: 0,
      isModalVisible: false,
      pickedCard: {}
    }
  },
  mounted() {
    console.log('card stack', this.cards)
    this.delta = this.getRandomNumber(0, 5)
  },
  methods: {
    showModal() {
      this.isModalVisible = true
    },
    closeModal() {
      this.isModalVisible = false
    },
    getRandomNumber(min, max) {
      return Math.round(Math.random() * (max - min) + min)
    },
    handlePickedCard(card, like) {
      this.pickedCard = card
      const currentCandidate = this.cards.indexOf(card)
      console.log(this.delta)
      console.log(like)
      console.log(currentCandidate)
      if (this.delta === currentCandidate && like) {
        console.log('THATS A MATCH!')
        this.showModal()
      }
    }
  }
}
</script>
<style lang="scss">
@import "~/assets/scss/main.scss";
  .noMore {
    text-align: center;
    display: flex;
    flex-flow: column wrap;
    height: 150px;
    justify-content: space-around;
    align-items: center;
    h3, h4 {
      font-family: 'PlayfairDisplayBold';
      font-size: 1.5em;
    }
    .btn-about {
        text-decoration: none;
        text-align: center;
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

@include mq-tablet {
  .tutorial {
    display: none;
  }
  .noMore {
    height: 400px;
    width: 200px;
    margin-top: 8em;
    justify-content: center;
    .btn-about {
      width: unset;
      margin-top: 1em;
    }
  }
}
</style>
