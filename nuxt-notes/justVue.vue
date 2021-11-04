When using in-DOM templates (templates directly written in an HTML file),
you should also avoid naming keys with uppercase characters,
as browsers will coerce attribute names into lowercase:


<template>
  <div>
    <!-- is="vue:someComponent" is dynamically render component, below is the same as <search-icon>...</search-icon> -->
    <div is="vue:search-icon"></div>

    <!-- Directives are special attributes with the v- prefix. reactively apply side effects to the DOM -->
    <p v-if="seen">Now you see me</p>

    <!-- argument", denoted by a colon after the directive name -->
    <a v-bind:href="url"> ... </a>
    <a v-on:click="doSomething"> ... </a>

    <!-- Dynamic argument v-on:[eventName] will be equivalent to v-on:focus -->
    <a v-on:[eventName]="doSomething"> ... </a>

    <!-- Add class in a object. Classname will be added if the value is TRUE -->
    <button
      type="button"
      class="reset-button search-icon"
      :class="{ 'search-trigger': isShowingSearchBar }"
    />

    <!-- v-bind shorthand-->
    <!-- full syntax -->
    <a v-bind:href="url"> ... </a>
    <!-- shorthand -->
    <a :href="url"> ... </a>
    <!-- shorthand with dynamic argument -->
    <a :[key]="url"> ... </a>

    <!-- v-on shorthand -->
    <!-- full syntax -->
    <a v-on:click="doSomething"> ... </a>
    <!-- shorthand -->
    <a @click="doSomething"> ... </a>
    <!-- shorthand with dynamic argument -->
    <a @[event]="doSomething"> ... </a>

  </div>
</template>

<script>
export default {
  // Vue uses a $ prefix when exposing its own built-in APIs via the component instance.
  // It also reserves the prefix _ for internal properties.

  // data function. these instance properties are only added when the instance is first created,
  // use null, undefined or placeholder value. until desired value is available.
  data() {
    return {
      count: 4
    }
  }
}
</script>

<style>

</style>
