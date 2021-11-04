
<template>
    <!-- inline class object -->
  <div
    class="static"
    :class="{ active: isActive, 'text-danger': hasError }"
  ></div>
</template>

<script>
  data() {
    return {
      isActive: true,
      hasError: false
    }
  }
</script>


<template>
  <div :class="classObject"></div>
</template>


<script>
export default {
  data() {
    return {
      isActive: true,
      error: null
    }
// return {
//   classObject: {
//     active: true,
//     'text-danger': false
//   }
// }
  },
  //Can also be written in the computed method
  computed: {
    classObject() {
      return {
        active: this.isActive && !this.error,
        'text-danger': this.error && this.error.type === 'fatal'
      }
    }
  }

}
</script>



<template>
  <!-- This will always apply errorClass, but activeClass will only be applied when isActive is truthy. -->
  <div :class="[isActive ? activeClass : '', errorClass]"></div>
  <!-- both are the same, can use object in array -->
  <div :class="[{ active: isActive }, errorClass]"></div>



  <!-- Adding class to component -->
  <!-- component with a single root element, those classes will be added to this element -->
  <div id="app">
    <my-component class="baz boo"></my-component>
  </div>

</template>

<script>
const app = Vue.createApp({})
app.component('my-component', {
  // multiple root elements, you would need to define which component will receive this class. You can do this using $attrs component property:
  template: `
  <p :class="$attrs.class">Hi!</p>
  <p class="foo bar">Hi!</p>
  `
  //If single root <p class="foo bar baz boo">Hi</p>
})
</script>



<template>
  <!-- Inline styling -->
  <div :style="{ color: 'red', fontSize: '12px' }"></div>

  <!-- using an object -->
  <div :style="styleObject"></div>

  <!-- Apply multiple style objects -->
  <div :style="[baseStyles, overridingStyles]"></div>
</template>


<script>
export default {
  data() {
    return {
      styleObject: {
        color: 'red',
        fontSize: '13px'
      }
    }
  }
}
</script>
