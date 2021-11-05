<template>
  <!-- v-if is a directive, -->
  <!-- A v-else element must immediately follow a v-if or a v-else-if element - otherwise it will not be recognized. -->
  <div v-if="Math.random() > 0.5">
    Now you see me
  </div>
  <div v-else>
    Now you don't
  </div>

  <!-- v-show will always be rendered and remain in the DOM; v-show only toggles the display CSS property of the element. -->
  <h1 v-show="ok">Hello!</h1>

  <!-- So prefer v-show if you need to toggle something very often, and prefer v-if if the condition is unlikely to change at runtime. -->
</template>



<template>
  <!-- V-for array, -->
  <!-- <div v-for="item in items" :key="index"> </div> -->
  <!-- second arg is the index -->
  <div v-for="(item, index) in items" :key="index.id"> </div>

  <!-- V-for Object, return all the value in the object -->
   <!-- <li v-for="value in myObject"> {{ value } </li> -->
   <!-- second arg is the key -->
   <li v-for="(value, name) in myObject" :key="name.id"> {{ name }}: {{ value }} </li>

  <!-- in v-for always provide a key attribute, use string or number  -->

  <!-- can use nested v-for with the computed method  -->
  <ul v-for="numbers in sets" :key="numbers.id">
    <li v-for="n in even(numbers)" :key="n">{{ n }}</li>
  </ul>

  <!-- can get the range of the number 1 to 10 -->
  <span v-for="n in 10" :key="n">{{ n }} </span>

  <!-- v-for on component, in order to pass the iterated data into the component, we should also use props: -->
  <my-component
    v-for="(item, index) in items"
    :item="item"
    :index="index"
    :key="item.id"
  ></my-component>
</template>
<script>
export default {
  data() {
    return {
      sets: [[ 1, 2, 3, 4, 5 ], [6, 7, 8, 9, 10]]
    }
  },
  methods: {
    even(numbers) {
      return numbers.filter(number => number % 2 === 0)
    }
  }
}
</script>

