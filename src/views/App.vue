<template>
  <div id="app">
    <div id="tab-notes" class="tab" :class="notesTabClass">
      <NotesHeader @onCreate="refreshNotes"></NotesHeader>
      <NotesList ref="list"> </NotesList>
    </div>

    <div id="tab-user" class="tab" :class="userTabClass">
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
  import NotesHeader from '../components/NotesHeader'
  import Navigation from '../components/Navigation'
  import NotesList from '../components/NotesList'


  Vue.use(Vuesax)
  Vue.use(VueRouter)

  export default {
    name: 'App',
    components: {Navigation, NotesHeader, NotesList},
    data() {
      return {
        notesTabClass: '',
        userTabClass: 'hidden',
      }
    },
    methods: {
      refreshNotes() {
        this.$refs.list.freshNotes()
      },

      switchTab(event) {
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

.tab {
  padding: 24px;
}
</style>