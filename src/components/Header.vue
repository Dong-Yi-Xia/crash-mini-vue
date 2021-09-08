<template>
  <header>
    <h1>{{ title }}</h1>
    <Button text="Add Task" color="green" />
  </header>
</template>

<script>
import Button from './Button.vue'

export default {
  name: 'Header', //Export name should be the same was the file name
  props: {
    title: String, //The props will be placed in the template as string interpolation
  },
  components: {
    Button,
  }
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
