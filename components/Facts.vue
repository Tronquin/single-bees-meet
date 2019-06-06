<template>
  <div class="facts">
    <p>Bee Fact #{{ factNumber }}: <span>"{{ facts }}"</span></p>
  </div>
</template>

<script>
import cheerio from 'cheerio'

export default {
  name: 'Facts',
  data: function () {
    return {
      facts: 'Hola',
      factNumber: 0
    }
  },
  mounted() {
    this.$axios.get('https://matteroftrust.org/20-amazing-honey-bee-facts/').then((response) => {
      if (response.status === 200) {
        const html = response.data
        const $ = cheerio.load(html)
        console.log('HTML', html)
        console.log('cheerio', $)
      }
    })
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";

.facts {
  background: $sunflower-black;
  width: 100%;
  height: 10vh;
  display: flex;
  justify-content: center;
  align-items: center;
  p{
    font-family: 'SourceSansBold';
    color: $sunflower-yellow;
    font-size: 1.1em;
    span {
      font-family: 'SourceSansLight';
      font-style: italic;
    }
  }
}
</style>
