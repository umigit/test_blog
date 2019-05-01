<template>
  <section class="container">
    <div class="input-box">
      <input v-model="message" class="text-box" type="text"/>
      <input class="submit-button" type="submit" @click="sendMessage"/>
    </div>
    <div class="message-box">
      {{message}}
    </div>
  </section>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue'
import firebase from 'firebase/app';

export default {
  components: {

  },
  data(){
    return {
      message: ""
    }
  },
  methods: {
    sendMessage() {
      return {
        message: ""
      }
    }
  }
}

</script>

<style>
.container {
  min-height: 100vh;
  text-align: center;
}

.input-box {
  display: inline-block;
  margin: 50px auto 0;
}

.text-box {
  width: 300px;
  height: 40px;
  border: 1px solid gray;
  padding: 10px 10px;
}

.submit-button {
  background-color: #22aaaa;
  width: 60px;
  height: 40px;
  border: 1px solid #22aaaa;
}

.message-box {
  width: 600px;
  border: 1px solid gray;
  margin: 10px auto;
  padding: 20px 40px;
}
</style>

