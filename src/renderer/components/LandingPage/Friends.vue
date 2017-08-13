<template>
  <div class="friends">
      
            <div class="form-group">
                <input type="text" placeholder="Введите имя..." class="form-control" id="search" v-model="search">
            </div>
  </div>
</template>

<script>
  import store from '@/store.js';

export default {
  data(){
      return store.friends;
  }
}
</script>


<style scoped>
.friends{
    position: absolute;
    width: 20vw;
    padding: 1vw;
}
</style>
