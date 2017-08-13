<template>
    <li class="card" @click="setDomain(friend.domain)">
        <avatar :src.sync="friend.photo_100"></avatar>
        <div>
            <h5>{{friend.name}}</h5>
            <h6>
                <a>@{{friend.domain}}</a>
            </h6>
        </div>
    </li>
</template>

<script>
  import store from '@/store.js';

import Avatar from '@/components/LandingPage/Avatar';


export default {
    props: ['friend'],
    components: { Avatar },
    methods:{

      setDomain(domain){
          console.log('click on', domain)
          store.main.domain = domain;
      }
    }
}
</script>
<style scoped>
.card{
    display: -webkit-box;
    cursor: pointer;
}
.card>div:first-child{
    width: 4vh;
    margin-right: 1vh;
}

</style>
