<template>
  <header>
    <div class="navbar-wrapper">
      <div class="logo-container">
        <span>Single</span>
        <span>Bees</span>
        <span>Meet</span>
      </div>
      <nav class="nav">
        <ul class="nav__links">
          <li>
            <a href="#">Dating</a>
          </li>
          <li>
            <a href="#">About</a>
          </li>
          <li>
            <a href="#">Resources</a>
          </li>
          <li>
            <a href="#">Contact</a>
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
    const nav = document.querySelector('.nav')
    menuToggle.onclick = () => {
      nav.classList.toggle('nav__open')
      hamburger.classList.toggle('open')
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/main.scss";

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: $sunflower-black;
  padding: 1em 0;
  position: relative;
  &::after {
    //content: '';
    clear: both;
    display: block;
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
      color: $sunflower-yellow;
    }
    .logo {
      width: 3.5em;
    }
    // &:hover {
    //   color: $sunflower-yellow-dark;
    // }
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
      background: $sunflower-yellow;
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
    }

    .open::before {
      opacity: 0;
    }

    .open::after {
      transform: rotate(-90deg) translate(3px);
    }
  }
}

@include for-tablet-portrait-up {
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
