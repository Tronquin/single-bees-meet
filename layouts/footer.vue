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
  background: #ffaf37;
  color: $sunflower-black;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 8vh;
}

@include mq-tablet {
  footer {
    .footer-headline {
      font-size: 1em;
    }
  }
}

@include mq-mobile-small {
    footer {
    .footer-headline {
      font-size: 0.7em;
    }
  }
}
</style>
