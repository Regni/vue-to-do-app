<script setup>
import { computed, ref } from 'vue'

const props = defineProps({
  todos: Array
})
const total = computed(() => props.todos.length)
const completed = computed(()=> props.todos.filter((todo)=> todo.completed ).length)
const percentageCompleted = computed(()=> total.value > 0 ? (completed.value / total.value * 100).toFixed(2) : 0)
</script>


<template>
  <div class="statsContainer">
    <table>
    <thead>
      <tr>
        <th>Total</th>
        <th>Completed</th>
        <th>Remaining</th>
        <th>Percentage of Completion</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>{{ total }}</td>
        <td>{{ completed }}</td>
        <td>{{ total - completed }}</td>
        <td>{{ percentageCompleted }}%</td>
      </tr>
    </tbody>
  </table>


   



   
  </div>
</template>


<style scoped>
.statsContainer{
  padding: 1rem;
  border-radius: 10px;
  border: 2px solid white
}
table{
  border-collapse: collapse;
 
}
th{
  background-color: black;
  border: 1px solid #ddd;
  padding: 12px 8px; 
}

td{
  padding: 12px 8px; 
  border: 1px solid #ddd;
}

</style>