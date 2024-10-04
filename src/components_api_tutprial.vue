<script setup>

import {ref, onMounted} from 'vue';

    const name = ref('Melkishi Tesfaye');
    const status = ref('active');
    const tasks = ref(['task one', 'task two', 'task three']);
    const newTask = ref('');

    const toggleStatus = () => {
      if (status.value == 'active') {
        status.value = 'pending';
      } else if (status.value == 'pending') {
        status.value = 'inactive';
      } else {
        status.value = 'active';
      }
    };

    const addTask = () => {
      if (newTask.value.trim() !== '') {
        tasks.value.push(newTask.value);
        newTask.value = '';
      }
    };

    const deleteTask = (index) => {
      tasks.value.splice(index, 1);
    };

    onMounted( async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map((task) => task.title);
      } catch (e) {
        console.log('Error occured')
      }
    })

</script>

<template>
  <h1>Vue Jobs</h1>
  <h2> {{ name }}</h2>
  <p v-if="status === 'active'">user is active</p>
  <p v-else-if="status === 'pending'">user is pending</p>
  <p v-else>user is inactive</p>

  <div>
    <form @submit.prevent="addTask">
      <label for="newTask">Add task</label>
      <br>
      <input type="text" id="newTask" name="newTask" v-model="newTask"/>
      <br>
      <button type="submit">Submit</button>
    </form>
  </div>

  <div>
    <ul>
      <li v-for="(task, index) in tasks" :key="task">
        <span>
          {{ task }}
        </span>
        <button  @click="deleteTask(index)"> Delete </button>
      </li>
    </ul>
    

  </div>

  <!-- <a :href="link">go to google</a> -->
  <br />
  <button @click="toggleStatus">Change Status</button>
</template>

<style scoped>
  h1 {
    color: red;
  }
</style>
