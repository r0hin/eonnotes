<template>
  <div class="about">
    <h1>You are signed in!</h1>
    <button @click="logOut()">Logout</button>
  </div>
</template>

<script>
  import Vue from 'vue'
  import VueRouter from 'vue-router'
  import Vuesax from 'vuesax'
  import 'vuesax/dist/vuesax.css'

  Vue.use(Vuesax)
  Vue.use(VueRouter)

  export default {
    name: 'App',
    components: {},
    data() {
      return {
        
      }
    },
    methods: {
      logOut() {
        const firebase = this.$firebase
        firebase.auth().signOut().then(() => {

        })
      }
    }
  }
</script>