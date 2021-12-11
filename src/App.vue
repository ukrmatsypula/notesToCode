<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <div id="app">
            <div class="message">
              <Message v-if="message" :message="message" />
            </div>

            <NewNote :note="note" @addNote="addNote" />
            <div class="note-header">
              <h1>{{ title }}</h1>

              <div class="icons">
                <svg
                  :class="{ active: grid }"
                  @click="grid = true"
                  class="icon icon--grid"
                >
                  <use xlink:href="./assets/sprite.svg#grid"></use>
                </svg>
                <svg
                  :class="{ active: !grid }"
                  @click="grid = false"
                  class="icon icon--column"
                >
                  <use xlink:href="./assets/sprite.svg#column"></use>
                </svg>
              </div>
            </div>

            <Notes :notes="notes" :grid="grid" @OnRemoveNote="removeNote" />
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message";
import NewNote from "@/components/NewNote";
import Notes from "@/components/Notes";

export default {
  name: "App",
  components: {
    Message,
    NewNote,
    Notes,
  },
  data: () => ({
    title: "Notes App",
    message: null,
    grid: true,
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
    removeNote(index) {
      this.notes.splice(index, 1);
    },
  },
};
</script>

<style></style>
