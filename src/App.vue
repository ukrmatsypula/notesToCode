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

              <Search
                :value="search"
                placeholder="Find your note"
                @search="onSearch"
              />

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

            <Notes
              :notes="notesFilter"
              :grid="grid"
              @OnRemoveNote="removeNote"
            />
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
import Search from "@/components/Search";

export default {
  name: "App",
  components: {
    Message,
    NewNote,
    Notes,
    Search,
  },
  data: () => ({
    title: "Notes App",
    search: "",
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
  computed: {
    notesFilter() {
      if (!this.search) {
        return this.notes;
      }

      return this.notes.filter((note) => {
        if (
          note.title.toLowerCase().indexOf(this.search.trim().toLowerCase()) !==
          -1
        ) {
          return note;
        }
        return this.arrayNotes;
      });
    },
  },
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
    onSearch(searchPayload) {
      this.search = searchPayload;
    },
  },
};
</script>

<style></style>
