<template>
  <div class="facts">
    <div v-for="(fact, index) in facts" :key="index" class="fact">
      <p>
        Bee Fact #{{ index }}:
        <span>"{{ fact }}"</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Facts',
  data: function () {
    return {
      facts: ''
    }
  },
  mounted() {
    this.facts = [
      'Approximately one third of the food we eat is the result of honey bee pollination',
      'In their 6-8 week lifespan, a worker bee will fly the equivalent distance of 1 ½ times the circumference of the Earth',
      'A productive queen can lay up to 2,500 eggs per day.',
      'Mead, which is made from fermented honey, is the world’s oldest fermented beverage.',
      'A single bee will produce only about 1/12 of a teaspoon of honey in its lifetime.',
      'Bees are attracted by caffeine.',
      'The perfect hexagons that form honeycomb hold the most amount of honey with the smallest amount of material (wax).',
      'Honey bees are the only insect that produces food consumed by humans.',
      'During a single collection trip, a honey bee will visit anywhere from 50 to 100 flowers.'
    ]
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";

.facts {
  margin-bottom: 1em;
  p {
    font-family: "SourceSansBold";
    color: $sunflower-black;
    font-size: 1.1em;
    span {
      font-family: "SourceSansLight";
      font-style: italic;
    }
  }
}
</style>
