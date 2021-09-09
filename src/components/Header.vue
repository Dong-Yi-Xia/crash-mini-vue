<template>
  <header>
    <h1>{{ title }}</h1>
    <!-- catch the generic btn with @btn-click and than emit same method name or different name  -->
    <Button
      @btn-click="$emit('toggle-add-task')"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="[showAddTask ? 'red' : 'green']"
    /> <!-- rather than text="regular string" when v-bind :text you can use JS logic --->
  </header>
</template>

<script>
import Button from './Button.vue'

export default {
  name: 'Header', //Export name should be the same was the file name
  props: {
    title: String, //The props will be placed in the template as string interpolation
    showAddTask: Boolean,
  },
  components: {
    Button,
  },
}
</script>

<style scoped> /*scoped - the css is only visible on this file template */
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>
