<template>
<footer>
  <p>Web Design and Content &copy; <a href="https://pilcrowmicro.com" target="_blank">Anthony McGrath</a>, October 2020</a></p>
</footer>
</template>

<script>
export default {
  name: 'Foot',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style lang="scss" scoped>
footer {
  padding: 1em;
  color: white;
  font-weight: 300;

  a {
    color: white;

    &:hover {
      text-decoration: underline;
    }
  }
}
</style>
