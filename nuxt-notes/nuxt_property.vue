// Prop names and event handler parameters
// DOM HTML Template use kebab-cased, components, fileNames
// camelCase in JavaScript

<template>

<!-- parent component -->
  <div>
    <!-- import the child. the emit must be grab with @ same function name that was emmited.  -->
    <!-- set = to another function to write out the logic in the methods.
    The payload will be the argument, changeLog(payload) -->
    <show-me-money  @display-money='changeLog'/>

    <!-- : is passing prop down = method/prop  -->
    <!-- @ is emit and grabbing that function name = method name to perform some actions (with payload) as arg-->
    <search-icon
      :is-showing-search-bar="isShowingSearchBar"
      @is-showing-search-bar-update="isShowingSearchBarUpdate"
    />
  </div>

</template>

<script>

export const MyComponent = Vue.extend({
  name: "MyComponent",
  components: { comp },
  props: {
    propA: Number,
    propB: {
      type: String,
      default: "default value",
    },
  },

  data() {
    return {
      sandwhich: "chicken",
      isRich: false
    }
  },

  methods: {
    findColor(){
      console.log("color")
    },

    displayMoney(event){
      //Emit takes a function to pass up, second is the payload
      //the function that takes the payload, it will be the passed in arugments
     this.$emit('displayMoney', event.target)
    }
  },

  watch: {
    isRich(newValue, oldValue){
      console.log(newValue, oldValue)
    }
  }

})

// nuxt-property-decorator
import { Component, Emit, Prop, Provide, Watch, Vue } from 'nuxt-property-decorator'

@Component({})
export class MyComponent extends Vue {
  @Prop()
  propA!: number

 @Prop({ default: "default value" })
  propB!: string

 //same as data(){}
 sandwhich = "chicken"
 isRich = false

 findColor(){
      console.log("color")
 }

 @Watch('isRich')
 someFunctionName(newValue, oldValue){
   console.log(newValue, oldValue)
 }

@Emit()
displayMoney(event){
  return event.target
}





// Emits
// parent component


}
</script>

<style>

</style>
