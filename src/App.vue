<template>
  <div id="app">
    <!-- <div :key="task.id" v-for="task in tasks">
      <p>{{task}}</p>
    </div> -->

    <AddTaskForm  @add-new-task="pushNewTask"></AddTaskForm>
    <div class="container">
      <b-row>
        <b-col md="4">
          <b-form-input v-model="filter" type="search" placeholder="Search Task"></b-form-input>
        </b-col>
      </b-row>
    </div>
    <BootstrapVueDatatable :posts="tasks" :filter="filter" @delete-task="deleteTask"></BootstrapVueDatatable>
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
      filter: ""
    }
  },
  methods: {
    async fetchAllTasks(){
      const res = await fetch ('http://localhost:5000/tasks')
      const data = await res.json()
      return data
    },
    async pushNewTask(task){
      
      const res = await fetch ('http://localhost:5000/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })
      const data = await res.json()
        this.tasks.push(data)
     
    },
    async deleteTask(id){
      console.log(`id to delete in deleteTask(id): ${id}`)
      const res = await fetch (`http://localhost:5000/tasks/${id}`, {
        method: 'DELETE',
        headers: {
          'Content-type': 'application/json',
        },
        
      })

      if (res.status === 200){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
      
     
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
