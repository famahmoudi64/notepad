<template>
<div class="container-fluid d-flex  justify-content-center" >
     <button class="btn btn-success mt-5 btn-plus" @click ="showNote">
        +AddNote
    </button>
</div>

<form @submit.prevent v-show="isShow">
    <div class=" container-fluid  mt-5" >
     <div class="row justify-content-center">
      <div class="col-lg-6 col-md-8 col-sm-10">
        <div class="card">
          <div class="card-body">
            <div class="form-group">
              <label for="input1" :style="{color:'green'}">Title:</label>
              <input type="text" class="form-control" id="input1" v-model="title">
            </div>
            <div class="form-group mt-2">
              <label for="textarea" :style="{color:'green'}">Description:</label>
              <textarea  class="form-control" row="3" id="textarea" v-model="desc"></textarea>
            </div>
        <div>
            <button class="ms-2 btn btn-success mt-3" @click="createNote" type="submit">Create</button>
            <button class="ms-2 btn btn-danger mt-3" @click="closeModel">Delete</button>
            <p class="mt-2" v-if="errorMessage" :style="{color:'red'}">you have to fill all input</p>
        </div>
      </div>
      </div>
      </div>
      </div>
     </div> 
    </form>
</template>

<script> 
export default{
    data(){
        return{
            title: "",
            desc: "",
            isShow: false,
            errorMessage: false
        }
    },
    methods:{
             createNote(){
               if(this.title.length > 0 && this.desc.length > 0){
                this.errorMessage = false
                const newNote = {
                    title : this.title,
                    description : this.desc
                }
                this.$emit('newNote',newNote)
                this.title = ""
                this.desc = ""
                this.isShow = false
                this.saveToLocal(newNote)
             }
              else {
                   this.errorMessage = true
                }
            },
             showNote(){
                this.isShow = true
             },
             closeModel(){
                this.isShow = false
             },
             saveToLocal(newNote){
              console.log(newNote)
              let notes;
              if(localStorage.getItem("notes") === null){
                  notes = []
                }else {
                    notes = JSON.parse(localStorage.getItem("notes")) 
                }
                  notes.push(newNote)
                    localStorage.setItem("notes",JSON.stringify(notes))
            },  
         },
        }

</script>
<style scoped>
.btn-plus{
    width:250px;
    font-size:30px;
    border-radius: 5px;  
}
</style>