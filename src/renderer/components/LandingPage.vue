<template>
  <div id="wrapper">
    <header>
      <img src="~@/assets/icon.png" class="logo" @click="open('https://vk.com/pingvk')"></img>
      <user></user>
  
    </header>
    <main>
      <h1 v-if="!this.user.authed" class="notauth">Вы не вошли </h1>
      <div v-else>
        <friends></friends>
        <main-block></main-block>
      </div>
    </main>
    <footer>
  
    </footer>
  </div>
</template>

<script>
import store from '@/store.js';
import User from '@/components/LandingPage/User';
import Friends from '@/components/LandingPage/Friends';
import MainBlock from '@/components/LandingPage/Main';
export default {
  data() {
    return store;
  },
  components: { User, MainBlock, Friends },
  methods: {
    open(link) {
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

.notauth {
  position: absolute;
  width: 20vw;
  left: 40vw;
  height: 20vh;
  top: 40vh;
  text-align: center;
}

.logo {
  width: 4vh;
  margin-left: 0.5vh;
  margin-top: 0.5vh;

  position: absolute;
  cursor: pointer;
}
</style>

