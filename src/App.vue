<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/repo">Repo</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
$main-background: #eee;
$main-black: #000;
$main-color: #6e4555;

body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: $main-background;
  color: $main-black;
}

#nav {
  a {
    color: $main-black;
    text-decoration: none;
    &.router-link-exact-active {
      color: $main-color;
    }
  }
}
</style>
