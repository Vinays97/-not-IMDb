<template>
<header>
    <router-link to="/">
        <h1><span>(not)</span>IMDb</h1>
    </router-link>
</header>
<main>
  <router-view/>
</main>
</template>

<style lang="scss">
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;

    &::selection {
      background: transparentize($color: #42b883, $amount: 0)
    }
}

body {
  background-color: #000000;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #121212;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);

  h1 {
    color: #ffffff;
    font-size: 28px;

    span {
      color: #f5c517;
    }
  }
}
</style>
