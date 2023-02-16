<!-- ! JavaScript Land -->
<!-- The setup keyword -->
<script setup>
// import dependencies from vue
import {ref, reactive} from 'vue'
/* 
    reactive - is similar to useState in React with limitations
    only applicable to objects including arrays

    ref - creates an object from any argument and creates an object 
    where the arugment can be found in the new object.value property
*/

const counter = reactive({
    count: 0
})

const message = ref("Lets count somethings...")

function add() {
    counter.count +=1
}

function sub() {
    counter.count -=1
}
</script>

<!-- ! HTML Land -->
<template>
<!-- use mustaches to excape HTML land {{ JavaScript Land }} -->
    <h1>{{message}}</h1>
    <h1>{{counter.count}}</h1>

    <!-- @click == onClick -->
    <h1>Variable Buttons</h1>
    <!-- passing the variable -->
    <button @click="counter.count++">Add</button>
    <button @click="counter.count--">Subtract</button>
    <br>
    <h1>Function Buttons</h1>
    <!-- passing a seperate function -->
    <button @click="add()">Add</button>
    <button @click="sub()">Subtract</button>

</template>

<!-- ! CSS Land -->
<!-- The scoped keyword will keep these styles scoped to this component -->
<style scoped>

</style>
