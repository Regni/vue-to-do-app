<script setup>
import { ref, computed, reactive } from 'vue'
import Stats from './components/Stats.vue';
// Här börjar vi koda...
// const showError = ref(false)
// const newToDoText = ref('')
// const todos = ref([{id:1 , text: "lär dig Vue",completed: false, priority:true}, {id:2, text: "Bygg en app", completed: true, priority:false}])
// const isDarkMode = ref(false)

const state = reactive({
  showError :false,
  newToDoText : "",
 todos : [{id:1 , text: "lär dig Vue",completed: false, priority:true}, {id:2, text: "Bygg en app", completed: true, priority:false}],
 isDarkMode:false
})


const addTodo = () => {
  if(!isValidTodo.value){
    state.showError = true
    return
  }

  state.showError = false
  state.todos.push({
    id: Date.now(),
    text: state.newToDoText,
    completed: false,
    priority: false
  })
  
state.newToDoText=""}

const isValidTodo = computed(() => {
  return state.newToDoText.length >= 4})


const togglePriority = (todo)=>{
 todo.priority = !todo.priority
}

const removeTodo =(todo)=>{
state.todos = state.todos.filter((item)=> item.id !== todo.id)
}

const toggleTheme  = ()=>{
  state.isDarkMode = !state.isDarkMode
}
</script>

<template>
  <header :class="{'dark-mode':state.isDarkMode}"><button @click="toggleTheme">{{ state.isDarkMode ? "☀️":"🌙" }}</button></header>
  <div class="app-container">
    <!-- Här börjar vi bygga... -->
     <div class="add-todo">
      <input type="text" v-model="state.newToDoText" :class="{'error': state.showError}" placeholder="Lägg till todo...">
      <button @click="addTodo" :disabled="!isValidTodo" >Lägg till</button>
     </div>
     <ul class="todo-list">
      <li v-for="todo in state.todos" :key="todo.id" class="todo-item" :class="{ 'completed': todo.completed, 'priority':todo.priority}">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{'done': todo.completed}">{{ todo.text }}</span>
        <div class="todo-actions">
        <span @click="togglePriority(todo)" style="cursor: pointer; margin-left: auto;">{{ todo.priority?'⭐': '☆' }}</span>
        <span @click="removeTodo(todo)" class="delete-btn">🗑️</span>
      </div>
      </li>
     </ul>
  </div>
  <Stats :todos="state.todos"/>
</template>

<style>
.app-container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #f0f0f0;
  border-radius: 8px;
  margin-bottom: 20px;
}

header.dark-mode {
  background-color: #333;
  color: white;
}

.theme-btn {
  padding: 8px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  background: white;
}

.theme-btn.dark {
  background: #666;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.add-todo input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.add-todo input.error {
  border-color: red;
}

.error-message {
  color: red;
  font-size: 0.9em;
  margin-top: -15px;
  margin-bottom: 15px;
}

.stats {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
  background: #f9f9f9;
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 20px;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  background: white;
  border: 1px solid #ddd;
  margin-bottom: 5px;
  border-radius: 4px;
  color: black;
}

.todo-item.completed {
  background: #57d11e;
}

.todo-item.priority {
  border-left: 6px solid gold;
}

.done {
  text-decoration: line-through;
  color: #888;
}

button {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  background: #4CAF50;
  color: white;
  cursor: pointer;
}

button:disabled {
  background: #cccccc;
  cursor: not-allowed;
}

.todo-actions {
  display: flex;
  gap: 8px;
  margin-left: auto;
}

.priority-btn, .delete-btn {
  padding: 4px 8px;
  border-radius: 4px;
  cursor: pointer;
}

.delete-btn {
  background-color: #ff4444;
}

.delete-btn:hover {
  background-color: #cc0000;
}


</style> 