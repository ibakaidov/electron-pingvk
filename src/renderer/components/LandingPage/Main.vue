<template>
    <div>
        <div class="form-group">
            <label for="domain">Какую страницу пингуем:</label>
            <input type="text" class="form-control" id="domain" v-model="domain">
        </div>
        <div class="form-group">
            <label for="message">Каким сообщением пингуем:</label>
            <input type="text" class="form-control" id="message" v-model="message">
        </div>
        <div class="form-group">
            <label for="repeats">Сколько раз пингуем:</label>
            <input type="number" class="form-control" id="repeats" v-model="repeats">
        </div>
    </div>
</template>

<script>

import store from '@/store.js';

export default {
data () {
    return store.main;
}  
}
</script>

