<template>
  <div class="new-note">
    <label>Title</label>
    <label>
      <input v-model="note.title" type="text">
      <label>Description</label>
      <textarea v-model="note.desc"></textarea>
    </label>
    <button class="btn btnPrimary" @click="addNote">Send</button>
  </div>
</template>

<script>
  export default {
    props: {
      note: {
        type: Object,
        required: true,
      }
    },
    methods: {
      addNote () {
        this.$emit('add-note', this.note)
      }

    }
  }
</script>

<style type="text/css">
  .new-note {
    text-align: center;
  }
</style>
