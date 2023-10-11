<template>

    <header>
      <h1>➖ToDo List➖</h1>
    </header>
    <main>
      <Testkomponente props=""/>  
      
<button @click="modalOn=!modalOn">➕ Neues ToDo</button>
      <form @submit.prevent="()=>todoSelected=false" v-if="todoSelected" >
        <input type="text" v-model="todoSelected.name" placeholder="Neue Aufgabe eingeben" />
        <input type="date" v-model="todoSelected.date" placeholder="Datum eingeben">
        <input type="time" v-model="todoSelected.time" placeholder="Zeit eingeben">
        <input type="submit" value="Add" />
      </form>
      <ul>
        <li v-for="(todo, index) in todoListe" :key="index">
          {{ todo.name }} - {{ todo.date }} - {{ todo.time }} - {{ todo.done ? 'Erledigt' : 'Offen' }}
          <div>
            <input type="checkbox" v-model="todo.done">
            <button @click.prevent="()=>todoSelected=todo" class="edit-button">🖋 Ändern</button>
          <button @click.prevent="deleteitem(todo.name)" class="delete-button">❌ Löschen</button>
          </div>
        </li>
      </ul>

      <div class="modal" v-if="modalOn">
      postion relative/absolute
background blurry, 
<form @submit.prevent="addtolist">
        <input type="text" v-model="newToDo.name" placeholder="Neue Aufgabe eingeben" />
        <input type="date" v-model="newToDo.date" placeholder="Datum eingeben">
        <input type="time" v-model="newToDo.time" placeholder="Zeit eingeben">
        <input type="submit" value="Add" />
      </form>
      </div>
    </main>

</template>

<script setup>
import { ref, onMounted } from 'vue';
import Testkomponente from './components/Testkomponente.vue';

const todoSelected = ref(false)
const todoListe = ref(getSavedTodoList())
const newToDo = ref({});
const modalOn =ref (false)

function getSavedTodoList() {
  const savedTodoList = localStorage.getItem('todoList');
  return savedTodoList ? JSON.parse(savedTodoList) : [
    { name: "Laub rechen", date: "5. Oktober", done: false },
    { name: "Badezimmer putzen", done: true },
    { name: "Zimmer aufräumen", done: false },
    { name: "Kuchen kaufen", done: false },
    { name: "Servietten kaufen", done: false }
  ];
}

function saveTodoList() {
  localStorage.setItem('todoList', JSON.stringify(todoListe.value));
}

onMounted(() => {
  
  todoListe.value = getSavedTodoList();
});

function addtolist() {
  console.log("exec");
  todoListe.value.push(newToDo.value);
  newToDo.value = {};
  saveTodoList(); 
}

function deleteitem(parameter) {
  console.log("delete function")
  todoListe.value = todoListe.value.filter(item => item.name !== parameter);
  saveTodoList(); 
}

</script>

<style scoped>
  header {
    background-color: #2c376b;
    padding: 15px;
    text-align: center;
    color: #ffffff;
    width: 100%;


  }

  main {
    width: 100%;
  }

  form {
    display: flex;
    margin-bottom: 10px;
    width: 100%;
  }

  input {
    margin-right: 10px;
    padding: 8px;
  }

  input[type="submit"] {
    background-color: #d35400;
    color: #ffffff;
    cursor: pointer;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    /* border: #d35400 solid 2px; */
    box-shadow: 0 0 4px 2px #d35400 ;
    background-color: rgb(250, 226, 195) ; 
    margin: 20px 0;
    padding: 10px;
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* color: white */
    
  }

  li button {
    background-color: #d35400;
    color: #ffffff;
    border: none;
    padding: 5px 10px;
    margin-left: 5px;
    cursor: pointer;
    border: none;
    border-radius: 5px;
  }

  .edit-button,.delte-button {
    background-color: #d35400;
    color: #ffffff;

  }



  .edit-button:hover {
    background-color: #27ae60;
    transition: 0.5s;
    box-shadow: 0 0 4px 2px black inset;
  }

  .delete-button:hover {
    background-color: #d30140 ;
    transition: 0.5s;
    box-shadow: 0 0 4px 2px black inset;
  }


</style>
