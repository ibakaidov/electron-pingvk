<template>
    <div class="main">
        <form>
            <div class="form-group">
                <label for="domain">Какую страницу пингуем:</label>
                <input type="text" class="form-control" id="domain" v-model="domain">
            </div>
            <div class="form-group">
                <label for="message">Каким сообщением пингуем (Для выведения цифр очередности добавьте ##):</label>
                <input type="text" class="form-control" id="message" v-model="message">
            </div>
            <div class="form-group">
                <label for="repeats">Сколько раз пингуем:</label>
                <input type="number" class="form-control" id="repeats" v-model="repeats">
            </div>

            <div class="form-group">
                <label for="timeout">С какой частотой пингуем (советуем указывать больше двух секунд):</label>
                <input type="number" class="form-control" id="timeout" v-model="timeout">
            </div>
            <button v-if="!this.work" type="button" class="btn btn-primary" @click="start">Начать</button>
            
        </form>
        <ping-log :logs.sync='logs'></ping-log>
    </div>
</template>

<script>
import vk from 'api.vk.com';

import store from '@/store.js';

import PingLog from '@/components/LandingPage/Main/Log';



export default {
    data() {
        return store.main;
    },
    components: {
        PingLog
    },

    methods: {
        start() {
            this.work = true;
            this.logs = [];
            this.crepeat = 0;
            if(this.message.indexOf('##')<0) {
                this.message+=" ##";    
            }
            this.timer = setInterval(this.tick, this.timeout*1000);
        },
        tick() {
            let message = this.message.replace('##', this.crepeat);

            vk('messages.send', { message, domain: this.domain, access_token: store.user.token }, (err, res) => {
                console.log(err, res);
            })
            this.logs.push(message);
            this.crepeat++;
            if (this.crepeat == this.repeats) {
                clearInterval(this.timer);
            }
        }
    }
}
</script>

<style scoped>
.main {
    width: 80vw;
    padding: 1vw;
    right: 0;
    position: absolute;
}
</style>
