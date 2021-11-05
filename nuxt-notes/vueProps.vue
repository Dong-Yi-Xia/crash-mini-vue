you'll want every prop to be a specific type of value.

<script>
export default {
  props: {
    title: String,
    likes: Number,
    isPublished: Boolean,
    commentIds: Array,
    author: Object,
    callback: Function,
    contactsPromise: Promise // or any other constructor
  }
}
</script>

<template>
  <!--  prop with no value will imply `true` -->
  <!-- If you don't set is-published's type to Boolean in props, it will be an empty string instead of "true" value. -->
  <blog-post is-published></blog-post>

  <!-- Dynamically assign to the value of a variable. -->
  <blog-post :is-published="post.isPublished"></blog-post>

  <!-- this is a JavaScript expression rather than a string. -->
  <!-- boolean -->
  <blog-post :is-published="false"></blog-post>
  <!-- array -->
  <blog-post :comment-ids="[234, 266, 273]"></blog-post>
  <!-- object -->
  <blog-post
  :author="{
    name: 'Veronica',
    company: 'Veridian Dynamics'
  }"
></blog-post>

</template>


<script>
//  one-way-down binding should NOT attempt to mutate a prop inside a child component.
export default {
  props: ['initialCounter', 'size'],
  // child component wants to use it as a local data, its' best to define a local data property that uses the prop as its initial value:
  data() {
    return {
      counter: this.initialCounter
    }
  },
  //  raw value that needs to be transformed, it's best to define a computed property using the prop's value:
  computed: {
    normalizedSize() {
      return this.size.trim().toLowerCase()
    }
}
</script>


<script>
export default {
  // Prop Type validation
  props: {
    // Basic type check (`null` and `undefined` values will pass any type validation)
    propA: Number,
    // Multiple possible types
    propB: [String, Number],
    // Required string
    propC: {
      type: String,
      required: true
    },
    // Number with a default value
    propD: {
      type: Number,
      default: 100
    },
    // Object with a default value
    propE: {
      type: Object,
      // Object or array defaults must be returned from
      // a factory function
      default() {
        return { message: 'hello' }
      }
    },
    // Custom validator function
    propF: {
      validator(value) {
        // The value must match one of these strings
        return ['success', 'warning', 'danger'].includes(value)
      }
    },
    // Function with a default value
    propG: {
      type: Function,
      // Unlike object or array default, this is not a factory function - this is a function to serve as a default value
      default() {
        return 'Default function'
      }
    },
  }
}
</script>

/* Types
String
Number
Boolean
Array
Object
Date
Function
Symbol
*/

// type can also be a custom constructor function and the assertion will be made with an instanceof check
<script>
  function Person(firstName, lastName) {
    this.firstName = firstName
    this.lastName = lastName
  }

  app.component('blog-post', {
    props: {
      author: Person,
      postTitle: String,
    }
}
</script>

<template>
  // In the DOM kebab-case the props
  <blog-post post-title="hello!"></blog-post>
</template>
