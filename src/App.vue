<script setup>
import {ref, watch} from 'vue'
let todos = ref(JSON.parse(window.localStorage.getItem('todos')))
let newTodo = ref('')
let filter = ref('all')

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
  window.localStorage.setItem('todos', JSON.stringify(value))}, {deep: true})

function activeFilter(todo) {
  return todo.complete == false
}


function todoFilter(todo) {
  if (filter.value === 'active') {
    return todo.complete === false;
  } else if (filter.value === 'completed') {
    return todo.complete === true;
  }
  return true;
}


</script>

<template>
<h1 id="welcome">My Todo</h1> 


<div id="blackbox">
  <ul>
    <li class="buttonThing" v-if="todos.length > 0">
      <p>{{ todos.filter(activeFilter).length }} items left</p>
      <button class="button" :class="{ 'active': filter === 'all' }" @click="filter = 'all'">All</button>
     <button class="button" :class="{ 'active': filter === 'active' }" @click="filter = 'active'">Active</button>
     <button class="button" :class="{ 'active': filter === 'completed' }" @click="filter = 'completed'">Completed</button>
   </li>
    <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}" class="flex-container">
      <input class="checkboxItem" type="checkbox" checked="checked" v-model="todo.complete"> 
    {{ todo.text }}
    <button @click="$event => deleteTodo(index)" class="deleteItem"></button>

    </li>

  </ul>


</div>

<input v-model="newTodo" @keydown.enter="todoButton" id="todoInput" placeholder="Write your todo" class="center-placeholder">
<!--   <button @click="todoButton" id="todoSubmit">Add Todo</button>  , add this for the todoSubmit -->



</template>



<style src="/src/vuestyle.css"></style>

