<template>
  <!-- EventListner  v-on:click  the shorthand is @click -->
  <button :style="{background: color}" class="btn" @click="onClickFun()"> {{text}} </button>
</template>

<script>
export default {
  name: 'Button',
  props:{
    text: String,
    color: String
  },
  methods:{
    onClickFun(){
      this.$emit('btn-click') //emit the generic method name btn-click
    }
  },
}
</script>
