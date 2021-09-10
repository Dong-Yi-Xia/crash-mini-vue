<template>
  <div class="container">
    <Header
      title="Task Tracker"
      @toggle-add-task="toggleAddTask"
      :showAddTask="showAddTask"
    />  <!--3.Embed the component, pass in the props -->
    <div v-show="showAddTask"> <!--v-if or v-show is a conditional statement -->
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    /> <!--v-bind an object/array the props tasks -->
  </div>
</template>

<script>
import Header from './components/Header.vue' //1.import the components
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header, //2. Register the components
    Tasks,
    AddTask,
  },
  data() { // the state
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },

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

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
