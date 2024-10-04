<script>
export default {
  data() {
    return  {
      name: 'Melkishi Tesfaye',
      status: 'other',
      tasks: ['task one', 'task two', 'task three'],
      link:'https://google.com',
    }
  },
  methods: {
    toggleStatus() {
        if (this.status == 'active') {
        this.status = 'pending';
      } else if (this.status == 'pending') {
        this.status = 'inactive';
      } else {
        this.status = 'active';
      }
    }
  }
}
</script>

<template>
  <h1>Vue Jobs</h1>
  <h2> {{ name }}</h2>
  <p v-if="status === 'active'">user is active</p>
  <p v-else-if="status === 'pending'">user is pending</p>
  <p v-else>user is inactive</p>

  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <a :href="link">go to google</a>
  <br />
  <button @click="toggleStatus"> Change Status </button>
</template>

<style scoped>
  h1 {
    color: red;
  }
</style>
