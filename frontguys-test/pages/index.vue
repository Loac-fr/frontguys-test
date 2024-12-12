<template>
  <div class="flex align-top">
    <div class="md:w-1/2">
      <h1 class="text-xxl md:text-[20vw] text-neutral-900">Register now</h1>
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
