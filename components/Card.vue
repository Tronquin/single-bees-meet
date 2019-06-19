<template>
  <div>
    <div v-for="(info, index) in beeInfo" :key="index" class="card-container">
      <div v-if="info.show" class="card">
        <img v-lazy="`img/${info.img}`" alt="bee-card">
        <div class="card-info">
          <h4 class="card-info-name">
            {{ info.name }}
          </h4>
          <h3 class="card-info-status">
            <fa :icon="fas.faLocationArrow" /> {{ info.status }}
          </h3>
          <div class="card-info-more-icon">
            <fa :icon="fas.faMapMarkerAlt" />
          </div>
        </div>
      </div>
      <transition v-if="info.showMoreInfo" name="fade">
        <div class="card-info-more-modal">
          <img v-lazy="`img/${info.img}`" alt="bee-more-info">
          <h4>{{ info.name }}</h4>
          <p>{{ info.info }}</p>
          <button>Help Us!</button>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import { fas } from '@fortawesome/free-solid-svg-icons'
export default {
  name: 'Card',
  props: {
    info: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      beeInfo: {}
    }
  },
  computed: {
    fas() {
      return fas
    }
  },
  created() {
    this.beeInfo = this.info
    // this.beeInfo.forEach((element) => {
    //   console.log('url', element.imgRoute)
    // })
  }
}
</script>

<style lang="scss" scoped>
.card {
  img {
    width: 600px;
  }
}
</style>
