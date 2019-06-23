<script>
export default {
  name: 'Modal',
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
            {{ card.name }}

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
            <p>{{ card.description }}</p>
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
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999999;
  }

  .modal {
    background: $sunflower-orange;
    border-radius: 25px;
    overflow-x: auto;
    display: flex;
    height: 100%;
    flex-direction: column;
    text-align: center;
    &-body  {
      height: 100%;
      display: flex;
      flex-flow: column wrap;
      justify-content: space-around;
      p {
        font-family: 'SourceSansLight';
      }
    }
  }

  .modal-header,
  .modal-footer {
    padding: 15px;
    display: flex;
  }

  .modal-header {
    color:  white;
    justify-content: space-between;
  }

  .modal-footer {
    justify-content: flex-end;
  }

  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    border: none;
    font-size: 20px;
    padding: 20px;
    cursor: pointer;
    font-weight: bold;
    color: white;
    background: transparent;
  }

  .btn-green {
    color: white;
    background: white;
    border: 1px solid white;
    border-radius: 2px;
  }
</style>
