<template lang="pug">
v-card
  v-container(fluid grid-list-lg)
    v-layout(v-for="item in list" row wrap justify-space-between align-center)
      v-flex(6)
        span {{item.label}} 
      v-flex(6)
        span.display-1 {{item.value}}
</template>

<script>
export default {
  props: ['list'],
}
</script>

<style>

</style>
