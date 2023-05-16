<script setup>
import {ref, watch} from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
let newTodo = ref('')



function todoButton() {
  todos.value.push({
    text: newTodo.value,
    complete: false
  })
  newTodo.value=''
}
function deleteTodo(index) {
  todos.value.splice(index, 1)
}

watch(todos, function(value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep: true})
</script>

<template>
<h1 id="welcome">My Todo</h1> 

<div id="blackbox">
  <ul>
    <li v-for="(todo, index) in todos" :class="{completed: todo.complete}" class="flex-container">
      <input class="checkboxItem" type="checkbox" checked="checked" v-model="todo.complete"> 
    {{ todo.text }}
    <button @click="$event => deleteTodo(index)" class="deleteItem">X</button>

    </li>
  </ul>
</div>

<input v-model="newTodo" @keydown.enter="todoButton" id="todoInput">
<button @click="todoButton" id="todoSubmit">Add Todo</button>



</template>



<style src="/src/vuestyle.css"></style>

