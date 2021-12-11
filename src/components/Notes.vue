<template>
  <div class="notes">
    <div
      class="note"
      :class="{ full: !grid }"
      v-for="(note, index) in notes"
      :key="index"
    >
      <div class="note-header">
        <p class="note-title">{{ note.title }}</p>
        <p class="close" @click="removeNote(index)">x</p>
      </div>

      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Notes",
  props: {
    notes: {
      type: Array,
      require: true,
    },
    grid: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    removeNote(index) {
      this.$emit("OnRemoveNote", index);
    },
  },
};
</script>

<style lang="scss">
.notes {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}

.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: #fff;
  transition: all 0.3s linear;
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.05);
  z-index: 1;

  &.full {
    display: flex;
    flex-direction: column;
    text-align: center;
    align-items: center;
    width: 100%;
    transition: all 0.3s linear;
    position: relative;

    .note-title .close {
      position: absolute;
      padding: 20px;
      right: 0;
      top: 0;
      z-index: 1;
    }

    .close {
      position: absolute;
      right: 0;
      padding: 20px;
    }
  }

  &:hover {
    transform: translateY(-6px);
    transition: all 0.3s ease;
  }

  .close {
    cursor: pointer;
  }
}

.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  h1 {
    font-size: 32px;
  }

  p {
    color: #402caf;
    font-size: 22px;
  }

  .icon {
    margin-right: 12px;
    cursor: pointer;
    fill: gray;
    color: gray;

    &:last-child {
      margin-right: 0;
    }
    &.active {
      color: #402caf;
      fill: #402caf;
    }
  }
}

.control {
  cursor: pointer;
}

.note-body {
  p {
    margin: 20px 0;
  }

  span {
    font-size: 14px;
    color: #999;
  }
}
</style>
