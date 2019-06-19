<template>
  <div class="card-stack-container">
    <Card :info="cardsInfo" class="card-stack" />
  </div>
</template>

<script>
import Card from '../components/Card'
export default {
  name: 'Dating',
  components: {
    Card
  },
  data() {
    return {
      cardsInfo: {}
    }
  },
  created() {
    const json = {
      honey: {
        name: 'Honey',
        status: 'IN DANGER',
        info: 'One of the most common social insects on the planet, honey bees create colonies that can be as large as 80,000 individual insects, live in hives and create honey.',
        location: 'Somewhere',
        description: 'One of the most common social insects on the planet',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-1.jpg'
      },
      bumble: {
        name: 'Bumble',
        status: 'IN DANGER',
        info: 'Bumble bees are very large, black and yellow, bees that you see flying around your garden during the warmer months.',
        description: 'Bumble bees are very large, black and yellow',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-2.jpg'
      },
      leaf: {
        name: 'Leafcutter',
        status: 'IN DANGER',
        info: 'These bees are about 7 to 18mm in length and look like they are made from some light metal or are very dark in color.',
        description: 'hese bees are about 7 to 18mm in length and look like they are made from some light metal ',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-3.jpg'
      },
      carpen: {
        name: 'Carpenter',
        status: 'IN DANGER',
        info: 'Carpenter bees are tricky to spot, but you may see them flying around you if you are near their chosen nesting area.',
        description: 'Carpenter bees are tricky to spot',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-4.jpg'
      },
      mining: {
        name: 'Mining',
        status: 'IN DANGER',
        info: 'There’s about 1,200 species of bees in the Andrena family, most commonly called mining bees. They are very similar in their behavior as digger bees.',
        description: 'There’s about 1,200 species of bees in the Andrena family',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-5.jpg'
      },
      plaste: {
        name: 'Plasterer',
        status: 'IN DANGER',
        info: 'Plasterer bees are a little bigger than sweat bees, coming in around 10 – 18mm in length and also quite hairy-looking.',
        description: 'Plasterer bees are a little bigger than sweat bees',
        location: 'Somewhere',
        show: true,
        showMoreInfo: false,
        img: 'bee-card-7.jpg'
      }
    }
    const info = []
    for (const key in json) {
      if (json.hasOwnProperty(key)) {
        info.push(json[key])
      }
    }
    this.cardsInfo = info
  }
}
</script>

<style>

</style>
