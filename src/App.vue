<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <div id="app">
            <h1>{{ title }}</h1>

            <div class="message">
              <Message v-if="message" :message="message" />
            </div>

            <NewNote :note="note" @addNote="addNote" />

            <div class="notes">
              <div class="note" v-for="(note, index) in notes" :key="index">
                <div class="note-header">
                  <p class="note-header">{{ note.title }}</p>
                </div>

                <div class="note-body">
                  <p>{{ note.descr }}</p>
                  <span>{{ note.date }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message";
import NewNote from "@/components/NewNote";

export default {
  name: "App",
  components: {
    Message,
    NewNote,
  },
  data: () => ({
    title: "notes App",
    message: null,
    note: {
      title: "",
      descr: "",
    },
    notes: [
      {
        title: "First Note",
        descr: "Description for first note",
        date: new Date(Date.now()).toLocaleString(),
      },

      {
        title: "Second Note",
        descr: "Description for second note",
        date: new Date(Date.now()).toLocaleString(),
      },

      {
        title: "Third Note",
        descr: "Description for third note",
        date: new Date(Date.now()).toLocaleString(),
      },
    ],
  }),
  methods: {
    addNote() {
      const { title, descr } = this.note;
      if (title === "") {
        this.message = "title can't  be black";
        return false;
      }
      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
      });

      this.message = null;
      this.note.title = "";
      this.note.descr = "";
    },
  },
};
</script>

<style></style>
