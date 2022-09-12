<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>

  <main></main>
  <router-view />
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Ubuntu:wght@300;400;500;700&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Ubuntu", sans-serif;

  &::selection {
    background: transparentize($color: #42B883, $amount: 0.5)
  }
}

body{
  background-color: #1B2430;
}

a{
  text-decoration: none;
}

header{
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2a3441;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);
}
</style>
