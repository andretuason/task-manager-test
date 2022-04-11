<template>
  <div id="app">
    <!-- <div :key="task.id" v-for="task in tasks">
      <p>{{task}}</p>
    </div> -->
    <AddTaskForm  @add-new-task="pushNewTask"></AddTaskForm>
    <BootstrapVueDatatable :posts="tasks" ></BootstrapVueDatatable>
  </div>
</template>

<script>
import BootstrapVueDatatable from "./components/BootstrapVueDatatable"
import TaskForm from "./components/AddTaskForm.vue"
import AddTaskForm from "./components/AddTaskForm.vue"

export default {
  name: 'App',
  components: {
    BootstrapVueDatatable,
    TaskForm,
    AddTaskForm
},
  data(){
    return{
      tasks: [],
    }
  },
  methods: {
    async fetchAllTasks(){
      const res = await fetch ('http://localhost:5000/tasks')
      const data = await res.json()
      return data
    },
    async pushNewTask(task){
      
      console.log(task)
      const res = await fetch ('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()
        this.tasks.push(data)
     
    }
  },
  async created(){
    this.tasks = await this.fetchAllTasks()
    // console.log(this.tasks)

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
