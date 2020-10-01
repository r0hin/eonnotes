<template>
  <div id="app">

    <div id="tab-home" :class="homeTabClass">
      <h1>Home Tab</h1>
    </div>

    <div id="tab-notes" :class="notesTabClass">
      <h1>Notes Tab</h1>
    </div>

    <div id="tab-user" :class="userTabClass">
      <h1>User Tab</h1>
    </div>

    <Navigation @changedTab="switchTab"></Navigation>

  </div>
</template>

<script>
  import Vue from 'vue'
  import VueRouter from 'vue-router'
  import Vuesax from 'vuesax'
  import 'vuesax/dist/vuesax.css'

  // Custom Components
  import Navigation from '../components/Navigation'

  Vue.use(Vuesax)
  Vue.use(VueRouter)

  export default {
    name: 'App',
    components: {Navigation},
    data() {
      return {
        homeTabClass: '',
        notesTabClass: 'hidden',
        userTabClass: 'hidden',
      }
    },
    methods: {
      switchTab(event) {
        this.homeTabClass = 'hidden'
        this.notesTabClass = 'hidden'
        this.userTabClass = 'hidden'
        this[event + 'TabClass'] = ''
      },
    }
  }
</script>

<style scoped>
.hidden {
  display: none;
}
</style>