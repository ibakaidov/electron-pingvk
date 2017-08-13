<template>
  <div id="app">
    <landing-page></landing-page>
  </div>
</template>

<script>
  import LandingPage from '@/components/LandingPage'

  export default {
    name: 'vkping',
    components: {
      LandingPage
    }
  }
</script>

<style>
  body{
    margin: 0;
    padding: 0;
    overflow: hidden;
  }
</style>
