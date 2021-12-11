<template>
  <div class="new-note">
    <label for="title">title</label>
    <input type="text" id="title" v-model="note.title" />
    <label for="description">description</label>
    <textarea id="description" v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  name: "NewNote",
  props: {
    note: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    addNote() {
      this.$emit("addNote", this.note);
    },
  },
};
</script>

<style lang="scss">
.new-note {
  text-align: center;
}
</style>
