<template>
  <div id="app">
    <nav-bar-menu  v-bind:tasks="tasks"></nav-bar-menu>
    <show-tasks :tasks="tasks"
    @edit:task="updateTask"></show-tasks>
  </div>
</template>

<script>
import NavBarMenu from '@/components/NavBar'
import ShowTasks from '@/components/ShowTasks'
export default {
  name: 'App',
  components: {
    NavBarMenu,
    ShowTasks
  },
  data () {
    return {
      tasks: []
    }
  },
  methods: {
    updateTask (id, updatedTask) {
      this.tasks = this.tasks.map(task => task.id === id ? updatedTask : task)
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}
</style>
