<template>
<div id="app">
  <Masthead />
  <Navi />
  <main>
    <router-view></router-view>
  </main>
  <Foot />
</div>
</template>

<script>
import Masthead from '@/components/Masthead.vue'
import Navi from '@/components/Navi.vue'
import Foot from '@/components/Foot.vue'

export default {
  name: 'app',
  components: {
    Masthead,
    Navi,
    Foot
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;700&display=swap');

body {
  background: #ADA996;
  /* fallback for old browsers */
  background: -webkit-linear-gradient(to bottom, #EAEAEA, #236d7269, #236D72, #00316A);
  /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(to bottom, #EAEAEA, #236d7269, #236D72, #00316A);
  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  min-height: 100vh;
  height: 100%;
  width: 100%;
  padding: 0px;
  margin: 0px;
}

#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #00316A;
  display: flex;
  flex-direction: column;
  align-items: center;

  nav {
    display: flex;
    width: 100%;
    justify-content: center;
    background: none;
    border: solid 0px#236d7222;
    border-top-width: 1px;
    border-bottom-width: 1px;

    a {
      display: block;
      padding: 0.5em;
      color: #236d72;
      font-weight: 500;

      &.router-link-active,
      &:hover {
        background-color: #236d7222;
      }
    }
  }

  main {
    background-color: rgba(255, 255, 255, 0.9);
    min-width: 400px;
    max-width: 1024px;
    width: 80%;
    margin: 1em;

    .content {
      padding: 1em;
    }

    ul {
      list-style-type: none;

      li {
        margin: 0.2em;
      }
    }

    Table {
      Button {
        margin: 0px 5px;
      }
    }

  }
}
</style>
