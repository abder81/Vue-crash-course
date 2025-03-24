<!-- <script>
export default {
  name: 'App',
  data() {
    return {
      name: 'John Doe',
      status: 'active',
      Tasks: ['task 1', 'task 2', 'task 3'],
      link: 'https://www.google.com'
    }
  },

  methods: {
    toogleStatus() {
      if (this.status === 'active') {
        this.status = 'pending'
      } else {
        this.status = 'active'
      }
    }
  },
}

</script>

<template>
  <h1> {{ name }}</h1>
  <p v-if="status === 'active'"> User is Active</p>
  <p v-else> User is Pending</p>
  <ul>
    <li v-for="task in Tasks" :key="task"> {{ task }}</li>
  </ul>
  <a :href="link">click me!</a>

  <button @click="toogleStatus">Change status</button>

</template> -->

<script setup>
import { ref, onMounted } from 'vue';

const name = 'John Doe';
const status = ref('active');
const Tasks = ref([]);
const newTask = ref('');

const toggleStatus = () => {
  status.value = status.value === 'active' ? 'pending' : 'active';
};

const addTask = () => {
  Tasks.value.push(newTask.value);
  newTask.value = '';
};

const deleteTask = (index) => {
  Tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    const todos = data.slice(0, 10);
    Tasks.value = todos.map((task) => task.title);
  } catch (error) {
    console.log(error);
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is Active</p>
  <p v-else>User is Pending</p>
  
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" v-model="newTask">
    <button type="submit">Add Task</button>
  </form>
  
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in Tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ul>

  <button @click="toggleStatus">Change Status</button>
</template>
