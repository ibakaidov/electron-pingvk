<template>
  <div id="wrapper">
    <header>
    <user></user>
    </header>
    <main>
        <h1 v-if="!this.user.authed" class="notauth">Вы не вошли </h1>
        <main-block v-else></main-block>
    </main>
    <footer>

    </footer>
  </div>
</template>

<script>
  import store from '@/store.js';
  import User from '@/components/LandingPage/User';
  import MainBlock from '@/components/LandingPage/Main';
  export default {
    data () {
      return store;
    },
    components: { User, MainBlock },
    methods: {
      open (link) {
        this.$electron.shell.openExternal(link)
      }
    }
  }
</script> 

<style scoped>
  header {
    background: #6588AE;
    box-sizing: content-box;
    width: 100%;

    height: 5vh;
    padding: 1vh;
  }
  .notauth{
    position: absolute;
    width: 20vw;
    left: 40vw;
    height: 20vh;
    top: 40vh;
    text-align: center;
  }
</style>

