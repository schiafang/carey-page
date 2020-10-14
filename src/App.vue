<template>
  <div id="app">
    <div class="main-container">
      <div id="nav">
        <div>
          <router-link to="/">CAREY SUNG</router-link>
        </div>
        <div>
          <router-link to="/repo" class="nav-item">Repo</router-link>
        </div>
      </div>
      <router-view />
    </div>
  </div>
</template>

<style lang="scss">
$main-background: rgb(250, 250, 250);
$main-black: #000;
$main-color: #6e4555;

body {
  margin: 0;
  font-size: 16px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: $main-background;
  color: $main-black;
}

.main-container {
  perspective: 1px;
  transform-style: preserve-3d;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: scroll;
}

#nav {
  display: flex;
  letter-spacing: 1px;
  padding: 30px 15px 15px 15px;
  justify-content: space-between;
  // height: 150px;

  a {
    color: $main-black;
    text-decoration: none;

    &:hover {
      opacity: 0.8;
    }

    &.router-link-exact-active {
      color: $main-color;
    }
  }
}

.nav-item {
  margin-left: 30px;
}

@media screen and (min-width: 600px) {
  #nav {
    padding: 30px 100px;
    font-size: 1.5rem;
  }
}
</style>
