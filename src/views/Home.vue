<template>
    <!--v-if or v-show is a conditional statement -->
    <AddTask
      v-show="showAddTask"
      @add-task="addTask"
    />
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    /> <!--v-bind an object/array/boolean the props tasks, no v-bind on string props -->
</template>

<script>
import Tasks from '../components/Tasks.vue'
import AddTask from '../components/AddTask.vue'

export default {
  name: 'Home',
  props: {
    showAddTask: Boolean,
  },
  components:{
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
    }
  },
  methods: {
    async addTask(task){ //the parameter of task is the newTask in the $emit that was passed up
      const resp = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      })

      const data = await resp.json()
      console.log(resp)
      console.log(data)

      this.tasks = [...this.tasks, data]
    },

    async deleteTask(id){ //DELETE
      if(confirm('Are you sure?')){
        const resp = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        })

        resp.status === 200 ?
        (this.tasks = this.tasks.filter((task) => task.id != id)) :
        alert('Error deleting task')
      }
    },

    async toggleReminder(id){ //UPDATE
      const taskToToggle = await this.fetchTask(id)
      const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const resp = await fetch(`api/tasks/${id}`, {
        method: "PATCH",
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updateTask)
      })

      const data = await resp.json()

      this.tasks = this.tasks.map((task) => task.id === id ? data : task)
    },

    async fetchTasks() { //READ
      const resp = await fetch('api/tasks')
      const data = await resp.json()
      return data
    },

    async fetchTask(id) {
      const resp = await fetch(`api/tasks/${id}`)
      const data = await resp.json()
      return data
    },
  },
  async created() { //lifecycle method
    this.tasks = await this.fetchTasks()
  },
}
</script>
