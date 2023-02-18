<script setup>
import {ref, computed} from 'vue'
// form handling
// basic todo list
// unique id for todos
let id = 0
// newTodo input handler
const newTodo = ref('')
// initial todos
const todos = ref([
    {id: id++, text: 'Breakfast', done: true},
    {id: id++, text: 'Lunch', done: true},
    {id: id++, text: 'Dinner', done: false},
])
const hideCompleted = ref(false)
// filtered list of todos base on done value using the computed hook
const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

// add new todo
function addTodo() {
    todos.value.push({id: id++, text: newTodo.value})
    newTodo.value = ''
}
// delete a todo
function deleteTodo(todo){
    todos.value = todos.value.filter((curr) => curr !== todo)
}

</script>

<template>
 <!-- form handling -->
 <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
</form>
<!-- list for todos -->
<ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
        <!-- create input to check off todo -->
        <input type="checkbox" v-model="todo.done">
        <span :class="{ done: todo.done }">{{ todo.text }}</span>
        <button @click="deleteTodo(todo)">X</button>
    </li>
</ul>
<!-- toggle for hideCompleted -->
<button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
</button>

</template>

<style scoped>
.done{
    text-decoration: line-through;
}
</style>