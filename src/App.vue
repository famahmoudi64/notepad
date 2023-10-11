<template>
<create-notes  @newNote="addNote"></create-notes >
 <list-notes :notesl="notes" @deleteNote="deleteNote"></list-notes>
</template>

<script>
import CreateNotes from './components/CreateNotes.vue'
import ListNotes from './components/ListNotes.vue'
export default{
  components:{CreateNotes,ListNotes},
 data(){
  return{
    notes:[],
  }
 },
 mounted(){
    let notes;
    if(localStorage.getItem("notes") === null){
    notes = []
    }else {
    notes = JSON.parse(localStorage.getItem("notes")) 
    this.notes = notes
    }
      },
               
 methods:{
  addNote(newNote){
  this.notes.push(newNote)
  console.log("hello")
  console.log(this.notes)
  },
  deleteNote(index){
    var ifremove = confirm("are you sure to delete the note?")
    if(ifremove){
    this.notes.splice(index,1)
  }
  },
}
 }
 
</script>