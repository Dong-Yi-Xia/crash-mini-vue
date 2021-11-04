
<template>
  <div>
    <!-- is="vue:someComponent" is dynamically render component, below is the same as <search-icon>...</search-icon> -->
    <div is="vue:search-icon"></div>

    <!-- Directives are special attributes with the v- prefix. reactively apply side effects to the DOM -->
    <p v-if="seen">Now you see me</p>

    <!-- argument", denoted by a colon after the directive name -->
    <a v-bind:href="url"> ... </a>
    <a v-on:click="doSomething"> ... </a>

    <!-- Add class in a object. Classname will be added if the value is TRUE -->
    <button
      type="button"
      class="reset-button search-icon"
      :class="{ 'search-trigger': isShowingSearchBar }"
    />
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style>
