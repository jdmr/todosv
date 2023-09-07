<template>
    <div
        class="container mx-auto max-w-prose p-8 min-h-screen flex flex-col items-center justify-center"
    >
        <h1 class="text-5xl tracking-widest mb-8">TODOS</h1>
        <div class="flex gap-1">
            <input
                id="todo"
                v-model="todo"
                type="text"
                class="rounded-lg text-gray-800 p-2 text-xl tracking-wider"
                @keyup.enter="addTodo"
            />
            <button
                class="bg-gray-100 text-gray-800 py-2 px-4 rounded-lg text-xl tracking-wider flex items-center shadow shadow-pink-500 hover:shadow-lg hover:shadow-pink-700 transition-all"
                @click="addTodo"
            >
                <i class="i-mdi:plus h-6 w-6"></i>
                <div>ADD</div>
            </button>
        </div>
        <ul class="flex flex-col gap-2 mt-8 w-full">
            <li
                v-for="task in todos"
                :key="task.id"
                class="bg-pink-300 text-gray-800 text-4xl tracking-wider p-4 rounded-lg shadow flex justify-between"
            >
                <div>{{ task.task }}</div>
                <button
                    class="bg-pink-800 text-pink-100 rounded-full flex items-center p-2 hover:bg-pink-900 transition-all"
                    @click="deleteTodo(task.id)"
                >
                    <i class="i-mdi:delete"></i>
                </button>
            </li>
        </ul>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface Todo {
    id: string
    task: string
}

const todos = ref([] as Todo[])
const todo = ref('')

const addTodo = () => {
    todos.value.push({ id: Math.random().toString(), task: todo.value })
    todo.value = ''
    const input = document.getElementById('todo') as HTMLInputElement
    input.focus()
}
const deleteTodo = (todoID: string) => {
    todos.value = todos.value.filter((todo) => todo.id !== todoID)
}
</script>
