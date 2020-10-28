<template>
<nav class="navbar">
  <router-link exact to="/">Home</router-link>
  <router-link to="/add">
    <Icon type="md-add-circle" /> Add Car
  </router-link>
</nav>
</template>

<script>
export default {
  name: 'Navi'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>

</style>
