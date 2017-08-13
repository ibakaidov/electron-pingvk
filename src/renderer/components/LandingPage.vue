<template>
  <div id="wrapper">
    <header>
    <user></user>
    </header>
  </div>
</template>

<script>
  import store from '@/store.js';
  import User from '@/components/LandingPage/User';
  export default {
    data () {
      return store;
    },
    components: { User },
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
    width: 100%;
    height: 5vh;
    padding: 1vh;
  }
</style>

