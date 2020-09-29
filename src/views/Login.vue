<template>
  <div class="home">

    <div class="center content-inputs">
      <div class="content-title">
        <h1>Welcome Back!</h1>
      </div>
      <form>
          <vs-input primary v-model="value" placeholder="Email" />
          <br />
          <vs-input type="password" icon-after v-model="value2" placeholder="Password">
            <template #icon>
              <i class='bx bx-lock-open-alt'></i>
            </template>
          </vs-input>
      </form>  
      <br>
      <div class="submitdiv">
        <vs-button class="signbtn" @click="redirectToApp()">Login</vs-button> 
        <vs-button class="signbtn" @click="redirectToApp()">Sign Up</vs-button>
      </div>
<br>
    </div>

  </div>
</template>

<style>

.signbtn {
  display: inline-block;
}

.submitdiv {
  display: flex;
  align-items: center;
  justify-content: center;
}

.content-inputs {

  position: fixed;
  top: 50%; left: 50%;
  transform: translate(-50%, -50%);
  min-width: 80%;

  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  border-radius: 24px;
  background-color: #F4F7F8;
}

.content-title {
  background-color: #EEF2F6;
  width: 100%;
  text-align: center;
  border-radius: 24px;
  margin-bottom: 24px;
}
</style>

<script>
  import Vue from 'vue'
  import VueRouter from 'vue-router'
  import Vuesax from 'vuesax'
  import * as firebase from "firebase";
  import 'vuesax/dist/vuesax.css'

  Vue.use(Vuesax)
  Vue.use(VueRouter)
  Vue.use(firebase)

  const firebaseConfig = {
    apiKey: "AIzaSyBi2Vg9UQfkK7y7FEmEb4oySB0loDFNg0M",
    authDomain: "eonnote-78e57.firebaseapp.com",
    databaseURL: "https://eonnote-78e57.firebaseio.com",
    projectId: "eonnote-78e57",
    storageBucket: "eonnote-78e57.appspot.com",
    messagingSenderId: "424859217085",
    appId: "1:424859217085:web:c6894536bbad6254fa5bd4"
  };
  // Initialize Firebase
  firebase.initializeApp(firebaseConfig);

  export default {
    name: 'Login',
    components: {},

    methods: {
      redirectToApp() {
        this.$router.push({ path: '/app' });
      },
    }
  }
</script>
