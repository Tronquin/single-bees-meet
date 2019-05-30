<template>
  <footer>
    <h3 class="footer-headline">
      Single Bees Meet Buzz Copyright &copy; 2019
    </h3>
  </footer>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";
footer {
    background: $sunflower-black;
    color: $sunflower-yellow;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 14vh;
}
</style>
