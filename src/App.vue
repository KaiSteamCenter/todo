<script setup>
import {ref} from 'vue'
let todos = ref([])
let newTodo = ref('')



function todoButton() {
  todos.value.push(newTodo.value)
  newTodo.value=''
}
function deleteTodo(index) {
  todos.value.splice(index, 1)
}


</script>

<template>
<h1 id="welcome">My Todo</h1> 

<div id="blackbox">
  <ul>
    <li v-for="(todo, index) in todos">
      <button @click="$event => deleteTodo(index)">X</button>
    {{ todo }}
    </li>
  </ul>
</div>

<input v-model="newTodo" @keydown.enter="todoButton" id="todoInput">
<button @click="todoButton" id="todoSubmit">Add Todo</button>

</template>



<style src="/src/vuestyle.css"></style>

