<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <!--Message-->
          <Message v-if="message" :message="message"/>
          <!--New Note-->
          <NewNote
              :note="note"
              @add-note="addNote"
          />

          <div class="note-header">
            <h1>{{title}}</h1>
            <!--Search-->
            <Search
                :value="search"
                placeholder="Find your note"
                @search="search = $event"/>
            <div class="icons">
              <svg @click="grid = true" :class="{ active: grid }" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect></svg>
              <svg @click="grid = false" :class="{ active: !grid }" style="cursor: pointer" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line></svg>
            </div>
          </div>
          <!--note list-->
          <Notes
            :notes="notes"
            @remove="removeNode"
            :grid="grid "
          />
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import Message  from './components/Message'
import NewNote from './components/NewNote';
import Notes from './components/Notes'
import Search from "./components/Search";

export default {
  components: {
    Message, NewNote, Notes, Search
  },
  data () {
    return {
      title: 'Note App - Wise',
      search: '',
      message: null,
      grid: true,
      note: {
        title: '',
        desc: ''
      },
      notes: [
        {
          title: 'First Note',
          descr: 'Description first note',
          data: Date.now().toLocaleString()
        },
      ]
    }
  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search
      if (!search) return array
      // Small
      search = search.trim().toLowerCase()
      // Filter
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      // Error
      return array
    }
  },
  methods: {
    addNote() {
      // console.log(this.note.title, this.note.desc)
      let {title, desc} = this.note

      if (title === '')  {
        this.message = 'title can be lanng'
        return false
      }

      this.notes.push({
        title: title,
        descr: desc,
        data: Date.now().toLocaleString()
      })
      this.message = null
      this.note.title = ''
      this.note.desc = ''
    },
    removeNode(index) {
      this.notes.splice(index, 1)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.note-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: 36px 0;
}
</style>
