<template>
  <!-- v-bind:class have a reminder if true, second argu is the class name  -->
  <!-- can pass $emit as a method or pass it inline -->
  <div @click="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>{{task.text}}
      <i @click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{task.day}}</p>
  </div>
</template>


<script>
export default {
  name: 'Task',
  props: {
    task: Object
  },
  methods: {
    onDelete(id){
      this.$emit('delete-task', id) //$emit is sending the data up the level
    }
  },
}
</script>


<style scoped>
.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
