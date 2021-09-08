<template>
  <header>
    <h1>Task Tracker</h1>
  </header>
</template>

<script>
export default {
  name: 'Header', //Export name should be the same was the file name
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
