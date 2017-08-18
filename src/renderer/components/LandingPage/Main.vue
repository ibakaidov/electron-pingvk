<template>
    <div class="main">
        <form>
            <div class="form-group">
                <label for="domain">Какую страницу пингуем:</label>
                <div class="input-group">
                <span class="input-group-addon" id="basic-addon">@</span>
                <input type="text" class="form-control" id="domain" v-model="domain" placeholder="durov" aria-describedby="basic-addon">
                </div>
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
                <label for="timeout">С какой частотой пингуем (советуем указывать больше двух секунд, если пингуете больше 20 раз):</label>
                <input type="number" class="form-control" id="timeout" v-model="timeout">
            </div>
            <div class="form-group">
    
                <button v-if="!this.work" type="button" class="btn btn-primary" @click="start">Начать</button>
                <button v-else type="button" class="btn btn-danger" @click="stop">Остановить</button>
            </div>
            <div class="form-group" v-if="this.work">
                <div class="progress-bar" role="progressbar" :aria-valuenow="crepeat" aria-valuemin="0" :aria-valuemax="repeats" :style="{width:this.progressWidth}">
                </div>
            </div>
    
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

    computed: {
        progressWidth() {
            return (this.crepeat / this.repeats) * 100 + "%";
        }
    },

    methods: {
        start() {
            this.work = true;
            this.logs = [];
            this.crepeat = 0;
            if (this.message.indexOf('##') < 0) {
                
                this.message += " ##";
            }
            this.timer = setInterval(this.tick, this.timeout * 1000);
        },
        stop(){
            clearInterval(this.timer);
            this.work=false;
        },
        tick() {
            let message = this.message.replace('##', this.crepeat);

            vk('messages.send', { message, domain: this.domain, access_token: store.user.token }, (err, res) => {
                if(err){
            this.logs.push('Сообщения не отправленно, сработал спам фильтр :(');

                    return;
                }
            this.logs.push(message);
                
            })
            this.crepeat++;
            if (this.crepeat == this.repeats) {
                this.stop();
                let domain = this.domain;
                setTimeout(()=>{
                    this.lastMessage(domain);
                }, 3000);
            }
        },  
        lastMessage(domain){
            vk('messages.send', { message:"Я использовал для этого vk.com/pingvk ;)", domain, access_token: store.user.token }, (err, res) => {});

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
