<template>
  <header>
    <router-link to="/">
      <h1><span>Quick Search </span>Movies</h1>
    </router-link>
    <router-link to="/favorites">
      <button class="favorite">Favorites</button>
    </router-link>
  </header>
  <main></main>
  <router-view />
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
  &::selection {
    background: transparentize(#42b883, 0.5);
  }
}

body {
  background-color: #35495e;
}

a {
  text-decoration: none;
}

header {
  display: inline;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2c3d4e;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.2);

  h1 {
    color: #fff;
    font-size: 28px;
    display: inline;

    span {
      color: #42b883;
    }
  }
}

.favorite {
        width: 100%;
        max-width: 200px;
        float: right;
        background-color: #42b883;
        padding: 10px;
        border-radius: 8px;
        color: #fff;
        font-size: 14px;
        text-transform: uppercase;
        transition: 0.4s;
  }
</style>
