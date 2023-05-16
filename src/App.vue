<script setup>
import {ref, watch} from 'vue'

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
</script>

<template>
<h1>My Todo Application</h1>


<div v-for = "(todo, index) in todos" :class="{completed: todo.complete}">
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
  text-align: center;
}

.completed {
  text-decoration: line-through;
  color: gray;
}
</style>
