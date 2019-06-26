<script>
export default {
  name: 'Match',
  props: {
    card: {
      type: Object,
      default: () => {}
    }
  },
  methods: {
    close() {
      this.$emit('close')
    }
  }
}
</script>
<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div
        class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header
          id="modalTitle"
          class="modal-header"
        >
          <slot name="header">
            <button
              type="button"
              class="btn-close"
              aria-label="Close modal"
              @click="close"
            >
              x
            </button>
          </slot>
        </header>
        <section
          id="modalDescription"
          class="modal-body"
        >
          <slot name="body">
            <img v-lazy="`img/${card.img}`" alt="modal-img" class="modal-match-img">
            <div class="modal-body-text">
              <h2>That's A Match!</h2>
              <div class="modal-body-text-white">
                <h2>Hi, my name is {{ card.name }}</h2>
                <h3>Here's a little information about me</h3>
                <p>{{ card.info }}</p>
                <p>If You are reading this, it's probably because my species is in danger of extinction, didn't you know? all bees are in danger! and without bees flowers can't exist! (neither humans), wanna know more?</p>
                <nuxt-link to="/about" class="btn-help">
                  Learn More
                </nuxt-link>
              </div>
            </div>
          </slot>
        </section>
      </div>
    </div>
  </transition>
</template>
<style lang="scss" scoped>
@import "~/assets/scss/main.scss";
 .modal-fade-enter,
  .modal-fade-leave-active {
    opacity: 0;
  }

  .modal-fade-enter-active,
  .modal-fade-leave-active {
    transition: opacity .5s ease
  }
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.500);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999999;
  }

  .modal {
    background: $sunflower-yellow-dark;
    box-shadow: 2px 2px 20px 1px;
    overflow: hidden;
    width: 100%;
    height: 600px;
    position: relative;
    &-header {
      border: none !important;
      position: absolute;
      right: 0;
    }
    &-body {
    display: flex;
    height: 100%;
    &-text {
      margin-left: 2em;
      h2 {
        font-size: 3em;
        font-family: 'PlayfairDisplayBold';
        text-align: center;
        text-transform: uppercase;
      }
      &-white {
        background: white;
        border-radius: 25px;
        padding: 1em 3em;
        margin: 1em 0;
        display: flex;
        flex-flow: column wrap;
        justify-content: space-around;
        h2 {
        font-family: 'SourceSansBold';
        font-size: 2.5em;
        text-align: unset;
        text-transform: uppercase;
      }
      h3 {
                font-family: 'SourceSans';
        font-size: 1.5em;
      }
      p {
        font-family: 'SourceSansLight';
        font-size: 1.2em;
      }
      .btn-help {
        text-decoration: none;
        text-align: center;
        width: 50%;
        padding: 1em 3.5em;
        border-radius: 50px;
        background-color: $sunflower-blue;
        border: none;
        outline: none;
        font-family: "SourceSansBold";
        font-size: 1em;
        cursor: pointer;
        color: $sunflower-black;
        text-transform: uppercase;
        transition: 0.2s background-color ease-in-out;
        &:hover {
          background-color: $sunflower-orange;
        }
    }
      }
    }
    }
    &-match-img {
      width: 400px;
      border-radius: 25px;
      object-fit: cover;
    }
  }

  .modal-header {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    color: $sunflower-black;
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 0.5em;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: $sunflower-black;
    background: transparent;
    position: relative;
    z-index: 99999;
  }

  .btn-green {
    color: white;
    background: $sunflower-blue;
    border: 1px solid $sunflower-blue;
    border-radius: 2px;
  }

  @include mq-tablet {
    .modal {
      height: 100%;
            overflow-y: scroll;
                &-header {
      justify-content: flex-end;
      .btn-close {
        color: white;
      }
    }
        &-body {
          flex-flow: column wrap;
      margin-top: 6em;
      height: unset;
      .modal-match-img {
        width: 100%;
      }
      &-text {
        margin: unset;
        width: 100%;
        text-align: center;
        h2 {
          margin: 0.5em 0;
        }
        &-white {
          margin-top: 0;
          padding: 1em;
          h2 {
            margin: 0;
          }
          h3 {
            margin: 0.5em 0;
          }
          .btn-help {
            margin-top: 1em;
            width: unset;
          }
        }
      }
    }
    }

  }
  @include mq-mobile-small {
    .modal-match-img {
              height: 200px;
    }
  }
</style>
