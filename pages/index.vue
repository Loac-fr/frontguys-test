<template>
  <div class="align-top md:flex">
    <div class="md:w-1/2">
      <h1 class="text-xl my-2 p-2 font-bold text-neutral-900 md:font-normal md:m-0 md:text-[20vw] md:leading-tight">Register now</h1>
    </div>
    <div class="bg-green-200 md:w-1/2">
      <FormRegister/>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage'
})
</script>
