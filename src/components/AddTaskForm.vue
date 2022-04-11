<template>
 <div class="container">
   <!-- <button @click="toggleAdd" :class="show">Add Task?</button> -->
   <Header @toggleDisplayAddTask="toggleAdd"></Header>
   <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Task Name:"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="task.taskName"
          placeholder="Enter task name"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Duration in hours:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="task.durationHours"
          type="number"
          placeholder="Input a rough estimate"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Progress:" label-for="input-3">
        <b-form-select
          id="input-3"
          v-model="task.status"
          :options="status"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-4" label="Start Date:" label-for="input-4">
        <b-form-datepicker 
          id="input-4"
          v-model="task.startDate"
          required
        ></b-form-datepicker>
      </b-form-group>

      <b-form-group id="input-group-5" label="End Date:" label-for="input-5">
        <b-form-datepicker
          id="input-5"
          v-model="task.endDate"
          
        ></b-form-datepicker>
      </b-form-group>

      <b-form-group id="input-group-6" label="Comments:" label-for="input-6">
        <b-form-textarea
          id="input-6"
          v-model="task.notes"
          placeholder="Comments with regards to task"
          rows="3"
        max-rows="6"
        > </b-form-textarea>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>

  </div>
</template>


<script>
import Header from "./Header.vue"
export default {
  name: 'AddTaskForm',
  components: {
    Header
  },
  data() {
      return {
        // Note 'isActive' is left out and will not appear in the rendered table
        show: false,
        // form: {
        //   email: '',
        //   name: '',
        //   food: null,
        //   checked: []
        // },
        task:{
            taskName: null,
            durationHours: null,
            status: null,
            startDate:  null,
            endDate: null,
            notes: null
        },
        status: [
          'Not started',
          'In Progress',
          'Pending',
          'Finished'
        ],
        
        buttonText: 'Add Task'
        // foods: [{ text: 'Select One', value: null }, 'Carrots', 'Beans', 'Tomatoes', 'Corn'],
        // items: [
        //   { isActive: true, age: 40, first_name: 'Dickerson', last_name: 'Macdonald' },
        //   { isActive: false, age: 21, first_name: 'Larsen', last_name: 'Shaw' },
        //   { isActive: false, age: 89, first_name: 'Geneva', last_name: 'Wilson' },
        //   { isActive: true, age: 38, first_name: 'Jami', last_name: 'Carney' }
        // ]
      }
    },
     methods: {
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.task))
        this.$emit('add-new-task', this.task)
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.task.taskName = ''
        this.task.durationHours = ''
        this.task.status = null
        this.task.startDate = ''
        this.task.endDate = ''
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
      toggleAdd(){
        this.show = !this.show

      }
    }
    
}
</script>

<style scoped>
.container {
  text-align: left;
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 20px;
}
</style>