<template>
  <div class="container">
    <div class="layer layer-back">
      <span class="title">Hello</span>
    </div>
    <div class="layer-front">
      <span class="text"
        >sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
        enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
        aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit
        in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
        Excepteur sint occaecat cupidatat non proident, sunt in culpa qui
        offi</span
      >
      <img
        class="front-img"
        src="https://images.unsplash.com/photo-1543311467-0d04382a7f69?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80"
        alt=""
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "home",
};
</script>

<style lang="scss">
.layer-front {
  height: 100vh;
  font-size: 18px;
  position: absolute;
  top: 100px;
  right: 0;
  bottom: 0;
  left: 0;

  img {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
  }
}

.layer-back {
  margin-top: 100px;
  height: 100vh;
  font-size: 50px;
  text-align: center;
  transform: translateZ(-1px) scale(2);
  background-image: url('https://images.unsplash.com/photo-1444505465537-42c1e519902b?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80');
  background-position: center;
  background-size: cover;
  z-index: -1;
}

.title {
  position: relative;
  top: calc(50% - 100px);
  display: inline-block;
  padding: 0 15px;
  background-color: #6e4555;
}

.text {
  height: 100vh;
  position: relative;
  top: 50%;
  display: block;
  color: #fff;
  font-size: 1.2rem;
  padding: 0 100px;
}
</style>
