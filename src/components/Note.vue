<template>
  <div>
    <div class="fullNote animated faster" :class="{
      'hidden': hideFull,
      'fadeInUp': fullFadeTrue,
      'fadeOutDown': fullFadeFalse,
    }">
      <h1>{{ noteData.name }}</h1>
      <vs-button @click="closeNote" class="closeNote" danger flat>
        <i class="bx bx-message-alt-x"></i>
      </vs-button>

      <br> <br> <br> <br>

      <div :id="noteData.id + 'editor'"></div>

      <center>
        <vs-button @click="save"> Save </vs-button>
      </center>

      <br> <br> <br> <br> <br> <br> <br> <br>

    </div>
    <vs-card @click="showNote" class="note_content">
      <template #title>
        <h3>{{ noteData.name }}</h3>
      </template>
      <template #text>
        <p>{{ noteData.preview }}</p>
      </template>
      <template #buttons>
        <vs-button class="btn-delete" danger>
          <i class="bx bx-trash"></i>
        </vs-button>
        <vs-button class="btn-chat" primary>
          <i class="bx bx-message-square-edit"></i>
        </vs-button>
      </template>
    </vs-card>
  </div>
</template>

<script>
import Vue from "vue";
import Vuesax from "vuesax";
import Vuex from "vuex";
import EditorJS from '@editorjs/editorjs';

Vue.use(Vuesax);
Vue.use(Vuex);

export default {
  name: "Note",
  data() {
    return {
      hideFull: true,
      fullFadeTrue: true,
      fullFadeFalse: false,
      dataGen: false,
      editor: null,
    };
  },
  props: ["noteData"],
  methods: {
    async save() {
      const output = await this.editor.save()
      const database = this.$firebase.database();
      const user = this.$store.state.user;

      console.log(output);

      await database.ref(`users/${user.uid}/notes/${this.noteData.id}`).set({
        'content': output,
      });

      this.$vs.notification({
        color: "success",
        position: "top-right",
        title: "Saved",
        text: `${this.noteData.name} saved successfully.`,
      });

    },
    async showNote() {
      this.hideFull = false;
      this.fullFadeTrue = true;
      this.fullFadeFalse = false;

      if (!this.dataGen) {
        this.dataGen = true;
        const Header = require('@editorjs/header');
        const SimpleImage = require('@editorjs/simple-image');
        const Embed = require('@editorjs/embed');
        const CodeTool = require('@editorjs/code');
        const Quote = require('@editorjs/quote');
        const Marker = require('@editorjs/marker');

        // Generate database from firebase rtdb

        const database = this.$firebase.database();
        const user = this.$store.state.user;
        const snapshot = await database.ref(`users/${user.uid}/notes/` + this.noteData.id).once('value')
        const tools = {
          Marker: {
            class: Marker,
            shortcut: 'CMD+SHIFT+M',
          },
          image: SimpleImage,
          header: {
            class: Header,
            config: {
              placeholder: 'Enter a header',
              levels: [1, 2, 3, 4, 5],
              defaultLevel: 3,
              inlineToolbar: true,
            }
          },
          embed: {
            class: Embed,
            config: {
              services: {
                "youtube": true,
                "codepen": true,
                "imgur": true,
                "gyfcat": true,
                "twitch-video": true,
                "twitch-channel": true,
                "coub": true,
                "twitter": true,
                "instagram": true,
              }
            }
          },
          code: CodeTool,
          quote: {
            class: Quote,
            inlineToolbar: true,
            shortcut: 'CMD+SHIFT+O',
            config: {
              quotePlaceholder: 'Enter a quote',
              captionPlaceholder: 'Quote\'s author',
            },
          },
        }

        if (snapshot.val()) {
          this.editor = new EditorJS({
            holder: `${this.noteData.id}editor`,
            data: snapshot.val().content,
            tools: tools,
            logLevel: 'ERROR',
          });
        }
        else {
          this.editor = new EditorJS({
            holder: `${this.noteData.id}editor`,
            tools: tools,
            placeholder: "Time to write ✏️ 😀...",
            logLevel: 'ERROR',
          });
        }

        console.log(this.editor);

      }

    },
    closeNote() {
      this.fullFadeTrue = false;
      this.fullFadeFalse = true;
      
      setTimeout(() => {
        this.hideFull = true;
      }, 500);
    }
  },
};
</script>

<style scoped>
.hidden {
  display: none;
}

h1 {
  float: left;
  margin: 0px;
}

.closeNote {
  float: right;
  font-size: 18px;
}

.fullNote {
  position: fixed;
  width: 95.6%;
  height: 100%;
  left: 0px;
  top: 0px;
  background-color: white;
  z-index: 2;
  padding: 24px;
  overflow-y: auto;
}
</style>
