<!-- ! JavaScript Land -->
<script setup>
/* 
    The setup keyword the code in the script will execute every time
    an instance of the component is created.
    
    Any top-level bindings (including variables, function declarations, and imports) declared inside <script setup> are directly usable in the template

    Imports are exposed in the same fashion. This means you can directly use an imported helper function in template expressions
 */
// import dependencies from vue
import {ref, reactive, computed, onMounted, watch } from 'vue'
/* 
    reactive - is similar to useState in React with limitations
    only applicable to objects including arrays

    ref - creates an object from any argument and creates an object 
    where the arugment can be found in the new object.value property

    computed - tracks other reactive state used in its computation as dependencies.
    It caches the result and automatically updates it when its dependencies change.

    onMounted - it allows us to register a callback to be called at certain times of the component's lifecycle. 
    There are other hooks such as onUpdated and onUnmounted

    watch - can directly watch a ref, and the callback gets fired whenever ref's value changes
*/
// import a childComponent
import TodoBasic from './components/TodoBasic.vue';

const counter = reactive({ count: 0 })
const message = ref("Lets count somethings...")

function add() {counter.count +=1}
function sub() {counter.count -=1}

// conditional attributes 
const positive = ref("green")
const negative = ref("red")

// input handling
// use v-model="variable name" to short hand event.target handling
const text = ref("")

// onMounted example
const p = ref(null)
onMounted(()=> {
    p.value.textContent = "mounted"
})

const count = ref(0)
function watcher() {
    console.log("This is what happens when the watched ref changes")
}
// watch example
watch(count, watcher)
</script>

<!-- ! HTML Land -->
<template>
<!-- use mustaches to excape HTML land {{ JavaScript Land }} -->
    <p ref="p">Hello World</p>
    <h1>{{message}}</h1>

    <!-- condtional redering -->
    <!-- uses v-if, v-else-if, v-else the assignment is the conditonal expression -->
    <template v-if="counter.count > 0">
        <h1 v-bind:class="positive">{{counter.count}}</h1>
    </template>
    <template v-else>
        <h1 v-bind:class="negative">{{counter.count}}</h1>
    </template>
    

    <!-- @click == onClick -->
    <h1>Variable Buttons</h1>
    <!-- passing the variable -->
    <button @click="counter.count++">Add</button>
    <button @click="counter.count--">Subtract</button>
    <br>
    <h1>Function Buttons</h1>
    <!-- passing a seperate function -->
    <button v-on:click="add()">Add</button>
    <button v-on:click="sub()">Subtract</button>
    <br>
    <!-- input handling -->
    <input v-model="text">
    <p> Look at what you wrote: {{text}}</p>

    <!-- Use Child Component -->
    <TodoBasic />

    <h1>{{count}}</h1>
    <button @click="count++">Trigger Watch, check the console</button>
</template>

<!-- ! CSS Land -->
<!-- The scoped keyword will keep these styles scoped to this component -->
<style scoped>

/* classes for contional styling */
.green{
    color: green;
}

.red  {
    color: red;
}


</style>
