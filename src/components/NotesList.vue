<template>
    <div id="notesList">
        <p>Your Notes</p>

        <div id="notes">
            <div class="note animated fadeIn" v-for="note in this.notes" v-bind:key="note.id">
                <vs-card class="note_content">
                    <template #title>
                        <h3>{{ note.name }} </h3>
                    </template>
                    <template #text>
                        <p> {{note.preview}} </p>
                    </template>
                    <template #buttons>
                        <vs-button class="btn-delete" danger>
                            <i class='bx bx-trash' ></i>
                        </vs-button>
                        <vs-button class="btn-chat" primary>
                            <i class='bx bx-message-square-edit' ></i>
                        </vs-button>
                    </template>
                </vs-card>

            </div>
        </div>

    </div>
</template>

<script>
import Vue from 'vue'
import Vuesax from 'vuesax'
import Vuex from 'vuex'

Vue.use(Vuesax)
Vue.use(Vuex)

export default {
    name: 'NotesList',
    data() {
        return {
            notes: []
        }
    },
    mounted () {
        this.freshNotes()
    },

    props: [],
    methods: {
        async freshNotes() {
            const db = this.$firebase.firestore()
            const user = this.$store.state.user

            const doc = await db.collection('users').doc(user.uid).get()
            this.notes = doc.data().notes
        }
    }
}
</script>

<style scoped>
    .cardfooter {
        position: absolute;
        bottom: 12px;
        right: 12px;
    }
    div#notes { 
        margin-top: 48px;
        display: grid;
        justify-items: center;
        grid-gap: 12px;
        grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    }
    div#notes .note {  
        width: 300px;
        height: 200px;
    } 
</style>

<style>
    /* Not scoped */
    .note_content .vs-card {
        height: 200px;
    }

    .vs-card__buttons {
        position: absolute;
        bottom: 12px;
        right: 12px;
    }

    .vs-card__buttons i {
        font-size: 18px;
    }
</style>