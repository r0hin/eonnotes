<template>
    <div>
        <div class="fullNote animated fadeIn" :class="showFull">
            <h1>{{noteData.name}}</h1>
        </div>
        <vs-card @click="showNote" class="note_content">
            <template #title>
                <h3>{{ noteData.name }} </h3>
            </template>
            <template #text>
                <p> {{noteData.preview}} </p>
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
</template>

<script>
import Vue from 'vue'
import Vuesax from 'vuesax'
import Vuex from 'vuex'

Vue.use(Vuesax)
Vue.use(Vuex)

export default {
    name: 'Note',
    data() {
        return {
            showFull: 'hidden',
        }
    },
    props: ["noteData"],
    methods: {
        showNote() {
            this.showFull = ''
        }
    }
}
</script>

<style scoped>
    .hidden {
        display: none;
    }

    .fullNote {
        position: fixed;
        width: 100%; height: 100%;
        left: 0px; top: 0px;
        background-color: white;
        z-index: 2;
        padding: 24px;
    }

</style>