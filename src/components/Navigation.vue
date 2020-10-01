<template>
  <div class="nav">
    <div class="navitem">
      <vs-button @click="tabe('home')" class="btno" :class="activeHome">
        <i class='bx bxs-home'></i>
      </vs-button>
    </div>
    <div class="navitem">
      <vs-button @click="tabe('notes')" class="btno" :class="activeNotes">
        <i class='bx bxs-notepad'></i>
      </vs-button>
    </div>
    <div class="navitem">
      <vs-button @click="tabe('user')" class="btno" :class="activeUser">
        <i class='bx bxs-user-pin'></i> 
      </vs-button>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import Vuesax from 'vuesax'

Vue.use(Vuesax)

export default {
  name: 'Navigation',
  data() {
      return {
        activeHome: '',
        activeNotes: 'inactive',
        activeUser: 'inactive',
      }
    },
  props: [],
  methods: {
    tabe(tab) {
      this.$emit('changedTab', tab);
      switch (tab) {
        case 'home':
          this.activeHome = ''
          this.activeNotes = 'inactive'
          this.activeUser = 'inactive'
          break;
        case 'notes':
          this.activeNotes = ''
          this.activeHome = 'inactive'
          this.activeUser = 'inactive'
          break;
        case 'user':
          this.activeUser = ''
          this.activeHome = 'inactive'
          this.activeNotes = 'inactive'
          break;
        default:
          break;
      }
    }
  }
}
</script>

<style scoped>
  .inactive {
    background-color: #ffffff;
    color: rgb(65, 65, 65);
    font-size: 14px;
  }

  .btno {
    width: 70%;
    padding: 6px;
  }
  .nav {
    position: fixed;
    bottom: 0px; left: 0px;
    width: 100%; height: 90px;
    background-color: #F4F7F8;

    display: grid;
    grid-template-columns: auto auto auto;

  }

  .navitem {
    display: inline-block;
    text-align: center;
    display: flex;

    justify-content: center;
    align-items: center;
  }
</style>