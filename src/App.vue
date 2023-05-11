<script setup>
import {ref} from 'vue'

let todos = ref([])
let inp = ref('')

function addTodo () {
  todos.value.push(inp.value)
  inp.value = ''
}

function deleteTodo (index) {
  todos.value.splice(index, 1)
}
</script>

<template>
<h1>My Todo Application</h1>

<ul>
<li v-for = "(todo, index) in todos">
  <button @click="deleteTodo">X</button>
{{ index }}
{{ todo }}</li>
</ul>

<input v-model="inp" @keydown.enter="addTodo">
<button @click="addTodo">Add Todo</button>
</template>

<style>
 body{
  background-color: bisque;
}
</style>
