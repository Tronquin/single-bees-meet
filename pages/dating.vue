<template>
  <div class="dating">
    <Navbar />
    <WhatAreYou>
      <GameCardsStack />
    </whatareyou>
    <Footer />
  </div>
</template>

<script>
import Navbar from '../layouts/navbar'
import Footer from '../layouts/footer'
import WhatAreYou from '../components/WhatAreYou'
import GameCardsStack from '../components/GameCardsStack'
export default {
  name: 'Dating',
  components: {
    Navbar,
    Footer,
    WhatAreYou,
    GameCardsStack
  }
}
</script>

<style>

</style>
