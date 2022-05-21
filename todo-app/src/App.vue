<script setup>
    import {
        ref
    } from "vue";
    const STORAGE_KEY = 'todos'
    const newTodo = ref('')
    const todos = ref(JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]'))

    function addTodo() {
        todos.value.push({
            text: newTodo.value,
            id: Date.now(),
            done: false
        })
        newTodo.value = ""

        setStorage();
    }

    function setStorage() {
        localStorage.setItem('todos', JSON.stringify(todos.value))
    }

    function complate(id) {
        todos.value.map(todo => {
            if (todo.id === id) {
                todo.done = !todo.done
            }
        })
        setStorage()
    }

    function deleteTodo(index) {
        todos.value.splice(index, 1)
        setStorage()
    }

    function clearStorage() {
        localStorage.clear()
        todos.value.splice(0)
    }
</script>

<template>

    <div class="min-h-screen flex flex-col items-center bg-slate-800 text-slate-100 font-mono pt-10">
        <h1 class="text-4xl">Vue-3 Todo App</h1>
        <div>
            <form class="flex flex-col items-start" @submit.prevent="addTodo">
                <label>Yeni Todo </label>
                <input v-model="newTodo" type="text" placeholder="todo..."
                    class="bg-slate-800 p-2 outline-slate-400 outline outline-1">
                <button class="w-full bg-slate-500 mt-1 p-1">todo ekle</button>
            </form>
        </div>
        <div>
            <h1 class="text-lg underline">Todo List</h1>
            <div>
                <span class="block" v-if="todos.length === 0">Empty List</span>
                <ul v-for="(todo, index) in todos">
                    <li class="flex flex-row items-center w-60 justify-between p-1 border w-full"
                        :class="{ 'text-green-800' : todo.done }">
                        <button @click="deleteTodo(index)" class="text-red-400">delete</button>

                        {{todo.text}}
                        <svg v-if="todo.done === false" @click="complate(todo.id)" class="w-6 h-6" fill="none"
                            stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                        <svg v-if="todo.done === true" @click="complate(todo.id)" class="w-6 h-6" fill="none"
                            stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                        </svg>
                    </li>
                </ul>
                <button class="bg-slate-500 p-1 mb-0 mt-5 float-right" @click="clearStorage">Clear All Todos</button>
            </div>
        </div>
    </div>
</template>