<template>
  <todo-button> Add todo Something </todo-button>
</template>


// child componenet, todo-button componenet
<template>
  <button class="btn-primary">
    <slot>Default/Fallback </slot>
  </button>
</template>


<template>
  <!-- rendered HTML -->
  <button class="btn-primary">
    Add todo Something
  </button>

  <!-- if nothing was passed inside the component in the parent, fallback takes its place-->
  <!-- Slot is flexible in reusing code -->
   <button class="btn-primary">
    Default/Fallback
  </button>
</template>
