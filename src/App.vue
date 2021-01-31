<template>
  <div id="app">
    <search />
    <results />
  </div>
</template>

<script>
import search from './components/search.vue'
import results from './components/results.vue'

export default {

  name: 'App',
  components: {
    search,results
  }
}

</script>


