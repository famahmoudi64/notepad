<template>
    <div class="container-fluid mt-5">
      <div class="row justify-content-center" v-for="(note, index) in notesl" :key="index">
        <div class="col-lg-6 col-md-8 col-sm-10">
          <div class="card">
            <div class="card-body">
              <div>
                <p><span>title:</span> {{ note.title }}</p>
                <p><span>desc:</span> {{ note.description }}</p>
              </div>
              <div>
                <button class="btn btn-outline-danger" @click="deleteNote(index)">
                  <i class="bi bi-archive-fill"></i>
                </button>
                <button class="btn btn-outline-success ms-2" @click="editNote(index)">
                  <i class="bi bi-pencil-square"></i>
                </button>
              </div>
              <div class="container-fluid mt-5" v-if="activeEditButton === index">
                <div class="row justify-content-center">
                  <div class="col-lg-6 col-md-8 col-sm-10">
                    <div class="card">
                      <div class="card-body">
                        <div class="form-group">
                          <label for="input1" :style="{ color: 'green' }">Title:</label>
                          <input type="text" class="form-control" id="input1" v-model.trim="note.title" />
                        </div>
                        <div class="form-group mt-2">
                          <label for="textarea" :style="{ color: 'green' }">Description:</label>
                          <textarea class="form-control" row="3" id="textarea" v-model.trim="note.description"></textarea>
                        </div>
                        <button @click="saveNote(index,note)">Save</button>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['notesl'],
    data() {
      return {
        activeEditButtonIndex: -1,
      };
    },
    computed: {
      activeEditButton() {
        if (this.activeEditButtonIndex !== -1) {
          return this.activeEditButtonIndex;
        }
        return null;
      },
    },
    methods: {
      editNote(index) {
        this.activeEditButtonIndex = index;
      },
      deleteNote(index) {
        this.$emit('deleteNote', index);
        this.deleteFromLocal(index);
      },
      saveNote(index,note){
        this.activeEditButtonIndex = -1
       this.editLocal(note,index)
    },
      deleteFromLocal(index) {
        let notes;
        if (JSON.parse(localStorage.getItem('notes') === null)) {
          notes = [];
        } else {
          notes = JSON.parse(localStorage.getItem('notes'));
        }
        notes.splice(index, 1);
        localStorage.setItem('notes', JSON.stringify(notes));
      },
      editLocal(note,index){
               let notes;
              if(localStorage.getItem("notes") === null){
                  notes = []
                }else {
                    notes = JSON.parse(localStorage.getItem("notes")) 
                }
                  console.log(notes[index])
                  notes[index]={
                    title:note.title,
                    description:note.description
                  }
                    localStorage.setItem("notes",JSON.stringify(notes))
            },  
        } 
        }  
        
</script>
<style scope>
span{
    color:green;
    font-size:18px;
}
.card{
    border-radius: 7px;
}
</style>