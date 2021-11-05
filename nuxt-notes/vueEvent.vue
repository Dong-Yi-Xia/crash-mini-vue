

// The usage (v-on or @) would be v-on:click="methodName" or with the shortcut, @click="methodName"

<template>
  <!-- original DOM event have a special $event variable greet($event)-->
  <button @click="greet">Greet</button>
  <button @click="warn('Form cannot be submitted yet.', $event)"> Submit </button>

  <!--Multiple event hander using comma both one() and two() will execute on button click -->
  <button @click="one($event), two($event)">Submit</button>

  <!-- event modifer - They can also be chain @click.stop.prevent-->
  <form @submit.prevent="onSubmit"></form>

  <!--  .passive communicates to the browser that you don't want to prevent the event's default behavior. -->
  <div @scroll.passive="onScroll">...</div>

  <!-- valid key names exposed via KeyboardEvent.key (opens new window)as modifiers by converting them to kebab-case. -->
  <input @keyup.page-down="onPageDown" />

  <!-- Common key
    .enter
    .tab
    .delete (captures both "Delete" and "Backspace" keys)
    .esc
    .space
    .up
    .down
    .left
    .right
  -->

  <!-- System control key -->
  <!-- Alt + Enter -->
  <input @keyup.alt.enter="clear" />

  <!-- Ctrl + Click -->
  <div @click.ctrl="doSomething">Do something</div>

  <!-- .exact key modifer -->
  <!-- this will fire even if Alt or Shift is also pressed -->
  <button @click.ctrl="onClick">A</button>

  <!-- this will only fire when Ctrl and no other keys are pressed -->
  <button @click.ctrl.exact="onCtrlClick">A</button>

  <!-- Mouse button modifier
  .left
  .right
  .middle
   -->
</template>

<script>
export default {
  methods: {
    warn(message, event) {
      // now we have access to the native event
      if (event) {
        event.preventDefault()
      }
      alert(message)
    }
  }
}
</script>
