<template>
  <div />
</template>

<script>
export default {
  name: 'WhatAreYou'
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";
.form {
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  height: 75%;
  width: 35%;
  border-radius: 50px;
  background: white;
  flex-flow: column wrap;
  color: $sunflower-yellow;
  .text-container {
    text-align: center;
    display: flex;
    justify-content: center;
    flex-flow: row wrap;
    .form-header {
      font-size: 2em;
      margin-bottom: 0.2em;
    }
    .form-subtitle {
      font-size: 1.2em;
      margin-bottom: 1em;
    }
    .dotted-divider {
      width: 90%;
      border: 1px dashed $sunflower-yellow;
    }
  }

  .what-are-you {
    display: flex;
    justify-content: space-around;
    width: 100%;
    font-size: 1.2em;
  }
}
</style>
