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
</script>

<template>
<h1>My Todo Application</h1>
<input name = "filter" type = "radio" value = "all" v-model="filter">
<label>All</label>

<input name = "filter" type = "radio" value = "active" v-model="filter">
<label>Active</label>

<input name = "filter" type = "radio" value = "complete" v-model="filter">
<label>Complete</label>

<div v-for = "(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}">
  <input type = "checkbox" v-model = "todo.complete">
  <button @click="deleteTodo(index)">x</button>
{{ todo.text }}
</div>

<input v-model="inp" @keydown.enter="addTodo">
<button @click="addTodo">Add Todo</button>
</template>

<style>
 body{
  background-color: bisque;
}

.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
