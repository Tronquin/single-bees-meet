<template>
  <div class="wrapper">
    <Navbar />
      <div class="wrapper-contact">
        <div class="wrapper-contact-form">
          <form>
            <h2>Contact</h2>
            <div class="form-field">
              <label for="name"></label>
              <input type="text" name="name" id="name" placeholder="Barry B. Benson">
            </div>
                        <div class="form-field">
              <label for="email"></label>
              <input type="email" name="email" id="message" placeholder="bee@honey.buzz">
            </div>
                        <div class="form-field">
              <label for="message"></label>
              <textarea name="message" id="message" cols="30" rows="10" placeholder="Wanna Pollinate?"></textarea>
            </div>
            <button type="submit">Send</button>
          </form>
        </div>
        <div class="wrapper-contact-talk">
          <h2>Wanna <span>Talk?</span></h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <h2>Wanna Talk?</h2>
          <img v-lazy="`img/${flower}`" alt="contact-flower">
        </div>
      </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from '../layouts/navbar'
import Footer from '../layouts/footer'
export default {
  name: 'Contact',
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      flower: 'main-sunflower.png'
    }
  }
}
</script>

<style lang="scss" scoped>
@import "~/assets/scss/main.scss";

.wrapper {
  &-contact {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80vh;
    &-form {
      width: 50%;
      align-self: flex-start;
      background-color: $sunflower-blue;
      border-radius: 25px;
      height: 100%;
      h2 {
        font-family: 'SourceSansBold';
        font-size: 3em;
        text-transform: uppercase;
      }
      form {
        display: flex;
        flex-flow: column wrap;
        justify-content: space-around;
        align-items: center;
        height: 100%;
        .form-field {
          width: 80%;
          input {
            width: 100%;
            border: none;
            border-radius: 50px;
            padding: 1em;
            outline: none;
            font-family: 'SourceSansLight';
            font-size: 1.2em;
          }
          textarea {
            width: 100%;
            border-radius: 25px;
            padding: 1em;
            outline: none;
            font-family: 'SourceSansLight';
            font-size: 1.2em;
          }
        }
        button {
          border: none;
          background-color: white;
          font-family: 'SourceSansBold';
          border-radius: 50px;
          padding: 0.2em 3em;
          font-size: 2em;
          cursor: pointer;
          transition: background-color ease 0.5s;
          &:hover {
            background-color: $sunflower-orange;
          }
        }
      }
    }
    &-talk {
      position: relative;
      h2 {
        text-transform: uppercase;
        font-family: 'PlayfairDisplayBold';
        font-size: 3em;
        letter-spacing: 0.2em;
        span {
          margin-left: 2em;
        }
      }
      img {
        position: absolute;
        width: 500px;
        top: 2em;
      }
    }
  }
}

@include mq-tablet {
  .wrapper {
    max-width: unset;
    padding: unset;
    margin: unset;
    &-contact {
      height: unset;
      justify-content: center;
      &-form {
        width: 100%;
        height: 80vh;
        margin: 1em;
      }
      &-talk {
        display: none;
      }
    }
  }
}

@include mq-mobile-small {
  .wrapper {
    &-contact {
      &-form {
        height: 100vh;
        margin: 0.5em;
      }
    }
  }
}
</style>
