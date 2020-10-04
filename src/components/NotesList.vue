<template>
  <div id="notesList">
    <p>Your Notes</p>

    <div id="notes">
      <Note
        class="note"
        :noteData="note"
        v-for="note in this.notes"
        v-bind:key="note.id"
      >
      </Note>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import Vuesax from "vuesax";
import Vuex from "vuex";

// Custom Components
import Note from "../components/Note";

Vue.use(Vuesax);
Vue.use(Vuex);

export default {
  name: "NotesList",
  data() {
    return {
      notes: [],
    };
  },
  mounted() {
    this.freshNotes();
  },
  components: { Note },
  props: [],
  methods: {
    async freshNotes() {
      const db = this.$firebase.firestore();
      const user = this.$store.state.user;

      const doc = await db
        .collection("users")
        .doc(user.uid)
        .get();
      this.notes = doc.data().notes;
    },
  },
};
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
  grid-gap: 56px;
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
  width: 100%;
}

.note {
  margin: 0px 8px 0px 8px;
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
