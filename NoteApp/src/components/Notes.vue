<template>
  <div class="notes">
    <div class="note" :class="{ full: !grid }" v-for="(note, index) in notes" :key="index">
      <div class="note-header">
        <p>{{note.title}}</p>
        <p @click="removeNode(index)" style="cursor: pointer">X</p>
      </div>
      <div class="note-body">
        <p>{{note.descr}}</p>
        <span>{{note.data}}</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      notes: {
        type: Array,
        required: true
      },
      grid: {
        type: Boolean,
        required: true
      }
    },
    methods: {
      removeNode (index) {
        console.log(`Note id: ${index}`)
        this.$emit('remove', index)
      }
    }
  }
</script>

<style lang="scss">
.notes {
  display: flex;
  align-content: center;
  justify-content: space-between;
  flex-wrap: wrap;
  padding: 40px 0;
}
.note {
  width: 48%;
  padding: 18px 20px;
  margin-bottom: 20px;
  background-color: white;
  &.full {
    width: 100%;
  }
}
.note-header {
  display: flex;
  align-content: center;
  justify-content: center;
}
.note-header h1 {
  font-size: 32px;
}
.note-header svg {
  margin-right: 12px;
  color: #999999;
  &.active {
    color: blue;
  }
}

.note-header svg:last-child {
  margin-right: 0;
}
.note-header p {
  color: blue;
  font-size: 22px;
}
.note-body p {
  margin: 20px 0;
}
.note-body span {
  font-size: 14px;
  color: #999;
}
</style>
