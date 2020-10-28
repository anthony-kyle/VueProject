<template>
<header>
  <img src="@/assets/logo.png" />
  <h3>Car Repo</h3>
</header>
</template>

<script>
export default {
  name: 'masthead',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
header {
  padding: 1em;
  color: #00316A;
  font-weight: bold;
  display: flex;
  flex-direction: column;

  img {
    width: 200px;
    height: auto;
    margin-bottom: 1em;
  }
}
</style>
