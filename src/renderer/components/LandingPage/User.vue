<template>
    <div class='user' :class="{authed:this.authed}" @click="login">
        <avatar :src.sync="avatar"></avatar>
    
    </div>
</template>

<script>

import OAuthVK from 'electron-oauth-vk';
import vk from 'api.vk.com';

import store from '@/store.js';

import Avatar from '@/components/LandingPage/Avatar';


const options = {
    clientID: 5775587,
    scope: ['messages', 'offline']
};

const oauth = new OAuthVK(require('electron').remote.BrowserWindow, options)

export default {
    data() {
        return store.user;
    },
    components: { Avatar },
    methods: {
        login() {
            if (this.authed) {


                return;
            }
            oauth.login().then(data => {
                this.authed = true;
                this.token = data.access_token;
                this.getUser();
            })

        },
        getUser() {
            vk('users.get', { access_token: this.token, fields: ['photo_200'] }, (err, res) => {

                if (err != null) return;
                let user = res[0];
                console.log(user);
                this.avatar = user.photo_200;
            })
        }
    }

}
</script>

<style scoped>
.user {
    position: absolute;
    right: 0;
    height: inherit;
    width: 10vh;
    border-top-left-radius: 5vh;
    border-bottom-left-radius: 5vh;
    background: #45688E;
    cursor: pointer;
}

.authed {

    animation-name: moveright;
    animation-duration: 2s;
    right: -5vh;
}

@keyframes moveright {
    from {
        right: 0vh;
    }
    to {
        right: -5vh;
    }
}
</style>
