<template>
          <ul class="log">
            <li v-for="log in logs" >{{log}}</li>     
        </ul>
</template>

<script>
export default {
  props:['logs']
}
</script>

<style scoped>


.log {
    list-style-type: none;
    border: 0.5px solid blanchedalmond;
    border-radius: 5px;
    padding: 5px;
    background: #ddd;
    height: 60vh;
    overflow: scroll;
    margin: 10px;
    margin-left: 0;
}
</style>
