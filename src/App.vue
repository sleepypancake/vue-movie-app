<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;

  &::selection {
    background: transparentize($color: #42B883, $amount: 0.5);
  }
}

body {
  background-color: #35495E;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2C3D4E;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);

  h1 {
    color: #fff;
    font-size: 28px;
  }

  span {
    color: #42B883;
  }
}

@media screen and (min-width: 1280px){
    .wrapper {
    margin: 0 20%;
  }
}

@media (min-width: 479px) and (max-width: 1279px){
    .wrapper {
    margin: 0 10%;
  }
}

</style>
