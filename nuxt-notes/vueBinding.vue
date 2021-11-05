// v-model directive to create two-way data bindings on form input, textarea, and select elements.

<template>
  <input type="text" v-model="message" placeholder="edit me" />
  <textarea v-model="text"></textarea>

  <!-- Array of checkbox item -->
  <input type="checkbox" id="checkbox" value="Yoyo" v-model="checked" />

  <!-- Single item for radio -->
  <input type="radio" id="one" value="One" v-model="picked" />

<!--  Recommended to provide a disabled option with an empty value -->
<!-- Adding multiple will return array of options -->
   <select v-model="selected" multiple>
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>

  <!-- Can use a v-for in the v-model -->
  <select v-model="selected">
    <option v-for="option in options" :key="option.id" :value="option.value">
      {{ option.text }}
    </option>
  </select>
  <span>Selected: {{ selected }}</span>

</template>

<script>
export default {
  data() {
    return {
      selected: 'A',
      options: [
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ]
    }
  }
}
</script>


<template>
  <!-- `picked` is a string "a" when checked -->
  <input type="radio" v-model="picked" value="a" />

  <!-- `toggle` is either true or false -->
  <input type="checkbox" v-model="toggle" />

  <!-- `selected` is a string "abc" when the first option is selected -->
  <select v-model="selected">
    <option value="abc">ABC</option>
  </select>

  <!-- lazy modifier - synced after "change" event instead of "input" event -->
  <input v-model.lazy="msg" />

  <!-- number modifier - automatically typecast as a number -->
  <input type="number" v-model.number="age"/>

  <!-- whitespace from user input to be trimmed automatically -->
  <input v-model.trim="msg" />

</template>
