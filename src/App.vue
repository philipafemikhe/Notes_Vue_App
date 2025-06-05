<script setup>
 import { ref } from 'vue';
 const showModal = ref(false);
 const newNote = ref("");
 const notes = ref([]);
 const errorMessage = ref("");

 function getRandomColor(){
 return "hsl(" + Math.floor(Math.random() * 360) +", 100%, 75%)";
 }

 const addNote = () =>{
  if(newNote.value.length < 10){
    errorMessage.value="Note must be minimum of 10 characters";
    return
  }
  notes.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newNote.value,
    date : new Date(),
    backgroundColor: getRandomColor()
  });
  showModal.value=false;
  newNote.value = "";
  errorMessage.value="";
 }
</script>

<template>
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
      <p v-if="errorMessage">{{ errorMessage }}</p>
      <button @click="addNote()">Add Note</button>
      <button class="close" @click="showModal = false">Close</button>

    </div>
  </div>
  <main>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal=true">+</button>
        <!-- <button class="close">Close</button> -->

      </header>
      <div class="cards-container">
        <div  v-for="note in notes" :key="note.id" class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date.toLocaleDateString("en-US") }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main{
    height: 100vh;
    widows: 100vw;
    background-color: #fafafc;
  }

  .container{
    max-width: 1000px;
    padding: 10px;
    margin:0 auto
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1{
    font-weight: bold;
    font-size: 75px;
    font-family:'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    color: black;
  }

  header button{
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: rgb(20,100,100);
    border-radius: 100%;
    color: aliceblue;
    font-size: 20px;
  }

  .card{
    width: 225px;
    height: 225px;
    background-color: rgb(211, 205, 190);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    color: rgb(2, 31, 31);
    float: left;
  }

  .date{
    font-size: 12.5px;
    font-weight: bold;
  }

  .card-container{
    display: flex;
    flex-wrap: wrap;
  }

  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.77);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: rgb(20,100,100);
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }

  .modal .close{
    background-color: red;
    margin-top: 7px;
  }

  .modal p{
    color: brown;
  }
</style>