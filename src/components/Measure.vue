<template>
  <div>
    <input type="feet" v-model="feet">feet
    <input type="inch" v-model="inch">inch
    <h2>this is feet {{feet}} this is inch {{inch}}</h2>
    <p v-if="typing">Typing...</p>
  </div>
</template>

<script>
export default {
  name: "Measure",
  data(){
    return{
      feet: "1",
      inch: "12",
      typing: false,
    }
  },
  watch: {
    //watch method name must be the same a data name
    feet(){
      this.typing = true
      this.inch = Number(this.feet ) * 12
      console.log("feet been changed")
      setTimeout(() => {this.typing = false}, 3000)
    },
    inch(){
      this.feet = Number(this.inch ) / 12
      console.log("inch been changed")
    }
  }
}
</script>

<style>
div{
  margin-top: 30px;
}
</style>
