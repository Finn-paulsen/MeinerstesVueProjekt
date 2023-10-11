<script setup>
import { ref } from 'vue';

const placeholder=[
  {name: "Banane", anzahl: 5, store: "Edeka", done: false},
  {name: "Mehl", anzahl: 4, store: "Aldi", done: true},
  {name: "Brot", anzahl: 2, store: "Edeka", done: false},
  {name: "Marmelade", anzahl: 5, store: "Edeka", done: false},
  {name: "Aufschnit", anzahl: 5, store: "Edeka", done: false}
]
const einkaufsliste = ref(placeholder)
const newitem = ref({done:false})
//{namen:"", anzahl:"", store:"", done:false}

function addtolist() {
  console.log("exec");
  einkaufsliste.value.push(newitem.value)
  newitem.value={}
}

function deleteItem(parameter) {
  console.log("deleteFunction")
  einkaufsliste.value=einkaufsliste.value.filter(item => item.name!=parameter)
}
</script>

<template>
  <header>
    <h1>To-Do-Liste</h1>
  </header>
  <main>
    <form>
      <input type="text" v-model="newitem.name">
      <input type="number" v-model="newitem.anzahl">
      <select name="store" v-model="newitem.store" id="store-select">
        <option value="">--Please choose an option--</option>
        <option value="edeka">Edeka</option>
        <option value="aldi">Aldi</option>
        <option value="rossmann">Rossmann</option>
        <option value="lidl">lidl</option>
        <option value="penny">Penny</option>
        <option value="netto">Netto</option>
        <option value="edeka">Edeka</option>
      </select>
      <input type="checkbox" v-model="newitem.done">
      <input type="button" value="Auf die Liste setzten" @click="addtolist" />
    </form>
    <p>{{ einkaufsliste }}</p>
    <article v-for="item in einkaufsliste">
      <div>{{item.name}}</div>
      <div>{{item.anzahl}}</div>
      <div>{{item.store}}</div>
      <div>{{item.done}}</div>
      <button @click.prevent="deleteItem(item.name)">Delete</button>
    </article>
  </main>
</template>

<style scoped>
article {
  display: flex;
  justify-content: space-between;
  box-shadow: 0 0 0 3px black;
}
</style>
