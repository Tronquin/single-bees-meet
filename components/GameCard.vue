<template>
  <div
    v-if="isShowing"
    ref="interactElement"
    :class="{
      isAnimating: isInteractAnimating,
      isCurrent: isCurrent,
      card: `'card-${index}'`
    }"
    class="card"
    :style="{ transform: transformString, 'background': `url('img/${card.img}') no-repeat center`, 'background-size': 'cover', 'object-fit': 'cover' }"
  >
    <div class="cardInfo">
      <div class="cardInfo-left">
        <h3 class="cardTitle">
          {{ card.name }}
        </h3>
      </div>
      <fa :icon="fas.faInfoCircle" class="card-moreInfo" @click="showModal" />
    </div>
    <modal
      v-show="isModalVisible"
      :card="card"
      @close="closeModal"
    />
  </div>
</template>

<script>
import { fas } from '@fortawesome/free-solid-svg-icons'
import interact from 'interactjs'
import modal from '../components/Modal'
const ACCEPT_CARD = 'cardAccepted'
const REJECT_CARD = 'cardRejected'
const SKIP_CARD = 'cardSkipped'

export default {
  name: 'GameCard',
  components: {
    modal
  },
  props: {
    card: {
      type: Object,
      default: () => {}
    },
    isCurrent: {
      type: Boolean,
      required: true,
      default: () => true
    },
    index: {
      type: Number,
      default: () => 0
    }
  },
  data() {
    return {
      isShowing: true,
      isInteractAnimating: true,
      isInteractDragged: null,
      interactPosition: {
        x: 0,
        y: 0,
        rotation: 0
      },
      isModalVisible: false
    }
  },
  static: {
    interactYThreshold: 250,
    interactXThreshold: 200
  },
  computed: {
    transformString() {
      if (!this.isInteractAnimating) {
        const { x, y } = this.interactPosition
        return `translate3D(${x}px, ${y}px, 0)`
      }
      return null
    },
    fas() {
      return fas
    }
  },
  mounted() {
    const element = this.$refs.interactElement
    interact(element, event).draggable({
      onstart: () => {
        this.isInteractAnimating = false
      },

      onmove: (event) => {
        const {
          interactMaxRotation,
          interactXThreshold
        } = this.$options.static
        const x = this.interactPosition.x + event.dx
        const y = this.interactPosition.y + event.dy

        let rotation = interactMaxRotation * (x / interactXThreshold)

        if (rotation > interactMaxRotation) rotation = interactMaxRotation
        else if (rotation < -interactMaxRotation) { rotation = -interactMaxRotation }

        this.interactSetPosition({ x, y, rotation })
      },

      onend: () => {
        const { x, y } = this.interactPosition
        const { interactXThreshold, interactYThreshold } = this.$options.static
        this.isInteractAnimating = true

        if (x > interactXThreshold) {
          this.playCard(ACCEPT_CARD)
          this.$emit('cardPicked', this.card, true)
        } else if (x < -interactXThreshold) {
          this.playCard(REJECT_CARD)
          this.$emit('cardPicked', this.card, false)
        } else if (y > interactYThreshold) {
          this.playCard(SKIP_CARD)
          this.$emit('cardPicked', this.card, false)
        } else {
          this.resetCardPosition()
        }
      }
    })
  },

  beforeDestroy() {
    interact(this.$refs.interactElement).unset()
  },

  methods: {
    showModal() {
      this.isModalVisible = true
    },
    closeModal() {
      this.isModalVisible = false
    },
    hideCard() {
      setTimeout(() => {
        this.isShowing = false
        this.$emit('hideCard', this.card)
      }, 300)
    },

    playCard(interaction) {
      const {
        interactOutOfSightXCoordinate,
        interactOutOfSightYCoordinate,
        interactMaxRotation
      } = this.$options.static

      this.interactUnsetElement()

      switch (interaction) {
        case ACCEPT_CARD:
          this.interactSetPosition({
            x: interactOutOfSightXCoordinate,
            rotation: interactMaxRotation
          })
          this.$emit(ACCEPT_CARD)
          break
        case REJECT_CARD:
          this.interactSetPosition({
            x: -interactOutOfSightXCoordinate,
            rotation: -interactMaxRotation
          })
          this.$emit(REJECT_CARD)
          break
        case SKIP_CARD:
          this.interactSetPosition({
            y: interactOutOfSightYCoordinate
          })
          this.$emit(SKIP_CARD)
          break
      }

      this.hideCard()
    },

    interactSetPosition(coordinates) {
      const { x = 0, y = 0, rotation = 0 } = coordinates
      this.interactPosition = { x, y, rotation }
    },

    interactUnsetElement() {
      interact(this.$refs.interactElement).unset()
      this.isInteractDragged = true
    },

    resetCardPosition() {
      this.interactSetPosition({ x: 0, y: 0, rotation: 0 })
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";

$cardsTotal: 6;
$cardsWidth: 400px;
$cardsPositionOffset: 55vh * 0.06;
$cardsScaleOffset: 0.08;
$defaultTranslation: $cardsPositionOffset * $cardsTotal;
$defaultScale: 1 - ($cardsScaleOffset * $cardsTotal);

.card {
  @include card();
  @include absolute(0);
  @include sizing(400px 80vw);
  @include flex-center();

  @include after() {
    @include sizing(21px 3px);
    @include absolute(right 0 bottom 11px left 0);

    margin: auto;
    border-radius: 100px;
  }
  z-index: 999;
  display: flex;
  max-height: 500px;
  margin: auto;
  font-size: 24px;
  font-weight: bold;
  color: white;
  // background-image: linear-gradient(
  //   -180deg,
  //   $sunflower-blue 2%,
  //   $sunflower-orange 100%
  // );
  opacity: 0;
  transform: translateY($defaultTranslation) scale($defaultScale);
  transform-origin: 50%, 100%;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  user-select: none;
  pointer-events: none;
  will-change: transform, opacity;

  height: 100vw;

  &.isCurrent {
    pointer-events: auto;
  }

  &.isAnimating {
    transition: transform 0.7s $ease-out-back;
  }

  &-moreInfo {
    cursor: pointer;
  }
}

.cardInfo {
    display: flex;
    margin-top: auto;
    -webkit-box-align: end;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1em;
    width: 100%;
    padding: 0 1em;
    .cardTitle {
      margin: 0;
      font-size: 1.5em;
    }
}

@for $i from 1 through $cardsTotal {
  $index: $i - 1;
  $translation: $cardsPositionOffset * $index;
  $scale: 1 - ($cardsScaleOffset * $index);

  .card:nth-child(#{$i}) {
    z-index: $cardsTotal - $index;
    opacity: 1;
    transform: translateY($translation) scale($scale);

    @if $i == 3 {
      color: red;
      background-color: red;
    } @else if $i == 2 {
      color: red;
      background-color: red;
    }

    @if $i != 1 {
      background-image: none;
      @include after() {
        @include sizing(0 0);
      }
    }
  }
}

</style>
