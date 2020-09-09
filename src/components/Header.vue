<template>
  <header class="header">
    <div class="logo">
      <h1>TodoList</h1>
      <img alt="Vue logo" src="../assets/logo.png" />
    </div>
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
  </header>
</template>

<script>
  export default {
    name: 'Header',
  }
</script>

<style scoped>
  .header {
    background: #333;
    color: #fff;
    text-align: center;
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .header a {
    color: #fff;
    padding-right: 5px;
    text-decoration: none;
  }

  .logo {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .logo img {
    width: 10%;
  }

  #nav {
    padding: 30px;
  }

  #nav a {
    font-weight: bold;
    color: #ffffff;
  }

  #nav a.router-link-exact-active {
    color: #42b983;
  }
</style>
