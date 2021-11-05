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
  },

  // You should avoid using arrow functions when defining methods, as that prevents Vue from binding the appropriate this value.
  methods: {
    increment() {
      // `this` will refer to the component instance
      this.count++
    }
  },

  // That's why for complex logic that includes reactive data, you should use a computed property.
  // A computed property will only re-evaluate when some of its reactive dependencies have changed.
  //  a method invocation will always run the function whenever a re-render happens.
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the vm instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  },

  // Watchers - This is most useful when you want to perform asynchronous or expensive operations in response to changing data.
  watch: {
    // whenever question changes, this function will run
    question(newQuestion, oldQuestion) {
      if (newQuestion.indexOf('?') > -1) {
        this.getAnswer()
      }
  }


}
</script>



// LifeCycle
<script>
const app = Vue.createApp({})
app.component('save-button', {
  created() {
    // Debouncing with Lodash
    this.debouncedClick = _.debounce(this.click, 500)
  },
  unmounted() {
    // Cancel the timer when the component is removed
    this.debouncedClick.cancel()
  },
  methods: {
    click() {
      // ... respond to click ...
    }
  },
  template: `
    <button @click="debouncedClick">
      Save
    </button>
  `
})
</script>




//Computed
<script>
Vue.createApp({
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  },
  computed: {
    // a computed getter
    publishedBooksMessage() {
      // `this` points to the vm instance
      return this.author.books.length > 0 ? 'Yes' : 'No'
    }
  },
  template: `
    <div id="computed-basics">
      <span>{{ publishedBooksMessage }}</span>
    </div>
  `
}).mount('#computed-basics')
</script>





// Watch method
<template>
  <div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question" />
  </p>
  <p>{{ answer }}</p>
</div>
</template>
<script>
  const watchExampleVM = Vue.createApp({
    data() {
      return {
        question: '',
        answer: 'Questions usually contain a question mark. ;-)'
      }
    },
    watch: {
      // whenever question changes, this function will run
      question(newQuestion, oldQuestion) {
        if (newQuestion.indexOf('?') > -1) {
          this.getAnswer()
        }
      }
    },
    methods: {
      getAnswer() {
        //When there is a ? response answer with Think...
        this.answer = 'Thinking...'
        axios
          .get('https://yesno.wtf/api')
          .then(response => {
            //After 2 sec, return an answer
            setTimeout(() => {this.answer = response.data.answer}, 2000)
          })
          .catch(error => {
            this.answer = 'Error! Could not reach the API. ' + error
          })
      }
    }
  }).mount('#watch-example')
</script>
