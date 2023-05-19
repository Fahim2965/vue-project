<script setup>
import {ref, watch} from 'vue'

let filter = ref('all')
let todos = ref(JSON.parse(window.localStorage.getItem('todos')) ?? [])
let inp = ref('')

watch(todos, function(value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, {deep: true})

function addTodo () {
  todos.value.push({text: inp.value,
  complete: false})
  inp.value = ''
}

function deleteTodo (index) {
  todos.value.splice(index, 1)
}


function todoFilter (todo) {
  if (filter.value == 'active') {
    return todo.complete == false
  } else if (filter.value == 'complete'){
    return todo.complete == true
  } else {
    return true
  }
}

function activeFilter (todo) {
  return todo.complete == false
}
</script>

<template>
<h1>My Todo Application</h1>

<p v-if = "todos.length > 0">
  <input name = "filter" type = "radio" value = "all" v-model="filter">
<label>All</label>

<input name = "filter" type = "radio" value = "active" v-model="filter">
<label>Active</label>

<input name = "filter" type = "radio" value = "complete" v-model="filter">
<label>Complete</label>
</p>

<input v-model="inp" @keydown.enter="addTodo">
<button @click="addTodo">Add Todo</button>


<p>{{ todos.filter(activeFilter).length }} Tasks left</p>
<div v-for = "(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}"> 
  <input type = "checkbox" v-model = "todo.complete">
{{ todo.text }}
<button @click="deleteTodo(index)">x</button>
</div>
   

</template>

<style>
 body{
  background-color: bisque;
  font-family: "Baloo 2", sans-serif;
}

.completed {
  text-decoration: line-through;
  color: gray;
}

input[type=checkbox] {
  -webkit-appearance: none;
  -moz-appearance: none;
       appearance: none;
  background-color: var(--form-background);
  margin: 0;
  font: inherit;
  color: currentColor;
  width: 1.15em;
  height: 1.15em;
  border: 0.15em solid currentColor;
  border-radius: 0.15em;
  transform: translateY(-0.075em);
  display: inline-grid;
  place-content: center;
}

input[type=checkbox]::before {
  content: "";
  width: 0.65em;
  height: 0.65em;
  -webkit-clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
          clip-path: polygon(14% 44%, 0 65%, 50% 100%, 100% 16%, 80% 0%, 43% 62%);
  transform: scale(0);
  transform-origin: bottom left;
  transition: 120ms transform ease-in-out;
  box-shadow: inset 1em 1em var(--form-control-color);
  background-color: CanvasText;
}

input[type=checkbox]:checked::before {
  transform: scale(1);
}

input[type=checkbox]:focus {
  outline: max(2px, 0.15em) solid currentColor;
  outline-offset: max(2px, 0.15em);
}

button {
      display: inline-block;
      font-size: 14px;
      font-weight: bold;
      padding: 8px 16px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      margin-right: 4px;
      text-align: center;
      text-decoration: none;
      text-transform: uppercase;
      transition: all 0.3s ease-in-out;
    }

    button:hover {
      background-color: #ff0000;
    }

    body {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Lato", "Lucida Grande", "Lucida Sans Unicode", Tahoma, Sans-Serif;
    }

</style>
