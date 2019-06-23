<template>
  <header>
    <div class="navbar-wrapper">
      <nuxt-link to="/">
        <div class="logo-container">
          <span>Single</span>
          <span>Bees</span>
          <span>Meet</span>
        </div>
      </nuxt-link>
      <nav class="nav">
        <ul class="nav__links">
          <li>
            <nuxt-link to="/dating">
              Dating
            </nuxt-link>
          </li>
          <li>
            <nuxt-link to="/about">
              About
            </nuxt-link>
          </li>
          <li>
            <nuxt-link to="/resources">
              Resources
            </nuxt-link>
          </li>
          <li>
            <nuxt-link to="/contact">
              Contact
            </nuxt-link>
          </li>
        </ul>
      </nav>
      <div class="menu-toggle">
        <div class="menu-toggle__hamburger" />
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Navbar',
  mounted() {
    const menuToggle = document.querySelector('.menu-toggle')
    const hamburger = document.querySelector('.menu-toggle__hamburger')
    const header = document.querySelector('header')
    const logo = document.querySelector('.logo-container')
    const nav = document.querySelector('.nav')
    menuToggle.onclick = () => {
      nav.classList.toggle('nav__open')
      hamburger.classList.toggle('open')
      header.classList.toggle('header-open')
      logo.classList.toggle('logo-open')
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";

.header-open {
  background: $sunflower-black;
}

.logo-open {
  span {
    color: $sunflower-yellow !important;
  }
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: #ffaf37;
  padding: 1em 0;
  position: relative;
  z-index: 99999;
  width: 100%;
  transition: background ease-in-out 0.8s;
  &::after {
    //content: '';
    clear: both;
    display: block;
  }
  a {
    text-decoration: none;
  }
  .logo-container {
    margin-left: 1.75em;
    display: flex;
    align-items: center;
    flex-flow: column wrap;
    justify-content: space-around;
    cursor: pointer;
    span {
      font-family: "SourceSansBold";
      font-size: 1.2em;
      color: $sunflower-black;
    }
    .logo {
      width: 3.5em;
    }
    // &:hover {
    //   color: $sunflower-yellow-dark;
    // }
  }
  .navbar-wrapper {
    max-width: 1160px;
    margin-right: auto;
    margin-left: auto;
    padding: 0 10px;
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .nav {
    width: 100%;
    position: absolute;
    top: 100%;
    right: 0%;
    background: $sunflower-black;
    clip-path: circle(0px at top);
    transition: all ease-in-out 500ms;
    &__links {
      li {
        border-bottom: 1px solid $sunflower-yellow;
        a {
          font-size: 1em;
          text-transform: uppercase;
          text-decoration: none;
          text-align: center;
          padding: 2em 6em;
          display: block;
          color: $sunflower-yellow;
          // &:hover,
          // &:focus {
          //   color: $sunflower-black;
          //   background: $sunflower-yellow-dark;
          // }
        }

        &:last-child {
          border-bottom: none;
        }
      }
    }

    &__open {
      clip-path: circle(150% at top);
    }
  }

  .menu-toggle {
    padding: 1em;
    position: absolute;
    right: 0.75em;
    cursor: pointer;

    &__hamburger,
    &__hamburger::before,
    &__hamburger::after {
      content: "";
      display: block;
      background: $sunflower-black;
      height: 3px;
      width: 1.75em;
      border-radius: 3px;
      transition: all ease-in-out 500ms;
    }

    &__hamburger::before {
      transform: translateY(-8px);
    }

    &__hamburger::after {
      transform: translateY(5px);
    }

    .open {
      transform: rotate(45deg);
      background: $sunflower-yellow;
    }

    .open::before {
      opacity: 0;
      background: $sunflower-yellow;
    }

    .open::after {
      transform: rotate(-90deg) translate(3px);
      background: $sunflower-yellow;
    }
  }
}

@include mq-mobile {
  header {
    background: none;
    justify-content: space-around;
    .logo-container {
      margin-left: unset;
      span {
        color: $sunflower-black;
      }
    }
    .nav {
      height: auto;
      width: auto;
      background: transparent;
      position: relative;
      clip-path: none;
      transition: none;
      &__links {
        display: flex;
        li {
          border-bottom: none;
          a {
            padding: 0 0 0 4em;
            color: $sunflower-black;
            // &:hover {
            //   background: $sunflower-black;
            //   color: $sunflower-yellow-dark;
            // }
          }
        }
      }
    }

    .menu-toggle {
      display: none;
    }
  }
}
</style>
