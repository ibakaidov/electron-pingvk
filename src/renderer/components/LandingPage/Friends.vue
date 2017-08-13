<template>
  <div class="friends">
      
            <div class="form-group">
                <input type="text" placeholder="Введите имя..." class="form-control" id="search" v-model="search">
            </div>
            <ul class="friends_list">
                <li v-for="item in friends" is="card" :friend.sync="item" ></li>
            </ul>
  </div>
</template>

<script>
import vk from 'api.vk.com';

  import store from '@/store.js';

  import Card from '@/components/LandingPage/Friends/Card';


export default {
  data(){
      return store.friends;
  },
  components:{Card},
  computed:{
      friends(){
          if (this.search == ''){
              return this.list;
          }
          return this.list.filter((v)=>{
              return v.name.toLowerCase().indexOf(this.search.toLowerCase())>-1;
          })
      }
  },
  methods: {
      getFriends(){
            vk('friends.get', { order:'hints', fields: 'photo_100,can_write_private_message,domain',  access_token: store.user.token }, (err, res) => {
            if (err!=null) return;
            this.list = res.map((item)=>{
              item.name = item.first_name+' '+item.last_name;
              return item;  
            });
            });
      }
  },
  mounted () {
      this.getFriends();
  }
}
</script>


<style scoped>
.friends{
    position: absolute;
    width: 20vw;
    padding: 1vw;
}
.friends_list{
    list-style: none;
    margin: 0;
    padding: 0;
    overflow-y: scroll;
    overflow-x: hidden;
    height: 80vh;
}
</style>
