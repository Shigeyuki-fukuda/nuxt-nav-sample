<template>
  <div>
    <Nav />
    <main></main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'
import Nav from '@/components/Nav.vue'

export default defineComponent({
  components: { Nav },
})
</script>
