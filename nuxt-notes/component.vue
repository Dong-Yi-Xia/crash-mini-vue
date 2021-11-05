<script>
  //Global component registration
  const app =Vue.createApp({})

  // With kebab-case - referencing only with kebab-case
  app.component('my-component-name', {})

  // With PascalCase - referencing both way <my-component-name> and <MyComponentName> are acceptable.
  app.component('MyComponentName', {})


</script>


module system with import/require and export
<script>
//local component registration
import ComponentA from './ComponentA'
import ComponentC from './ComponentC'

export default {
  components: {
    ComponentA,
    ComponentC
  }
}
</script>
