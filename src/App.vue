<template>
  <div id="app">
    <header class="header">
      <div class="header__inner">
        <router-link to="/">
          <img
            alt="Homeday logo"
            src="./assets/logo.svg"
            class="header__logo"
          />
        </router-link>
        <nav class="nav">
          <ul class="nav__container">
            <li class="navItem">
              <router-link to="/" class="navItem__link">Search</router-link>
            </li>
          </ul>
        </nav>
      </div>
    </header>
    <router-view />
  </div>
</template>

<style lang="scss">
.header {
  border-bottom: 1px solid lightgray;

  &__inner {
    max-width: 800px;
    margin: 0 auto;
    padding: 0 1rem;
  }

  &__logo {
    float: left;
    margin-top: 28px;
  }
}

.nav {
  padding: 30px;
  &__container {
    display: flex;
    list-style-type: none;
    margin: 0;
    padding-left: 20px;
  }
  .navItem {
    font-size: 0.9rem;
    margin-right: 1.3rem;
    text-decoration: none;
    &__link {
      font-weight: bold;
      color: #2c3e50;
      &.router-link-exact-active {
        color: #2988ff;
      }
    }
  }
}

body {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

main {
  margin: 0 auto;
  max-width: 800px;
  padding: 3rem 1rem;
  min-height: 70vh;
}

  }
}
</style>
