<script setup>
import {ref} from 'vue'

let todos = ref([])
let inp = ref('')

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


<div v-for = "(todo, index) in todos">
  <input type = "checkbox" v-model = "todo.complete">
  <button @click="deleteTodo(index)">X</button>
{{ index }}
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
</style>
