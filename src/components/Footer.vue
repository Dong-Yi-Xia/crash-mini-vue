<template>
  <footer>
    <p>Copyright &copy; 2021</p>
    <router-link to="/about">About</router-link> <!-- use the router-link and to rather than href, no page reload-->
  </footer>
</template>

<style scoped>
 a {
  color: #333;
}
footer {
  margin-top: 30px;
  text-align: center;
}
</style>
