<template>
    <div>
   <img v-if="src!=null" class="avatar" :src="src"></img>
   <img v-else class="avatar" src="~@/assets/dog.png"></img>
       </div>
</template>

<script>
export default {
  props:['src']
}
</script>

<style scoped>

    .avatar {
        width: 4vh;
        height: 4vh;
        border-radius: 4vh;
        margin-left: 0.5vh;
        margin-top: 0.5vh;
    }
</style>
