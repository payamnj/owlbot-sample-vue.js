<template>
  <div v-if="this.response">
      <WordItem  v-for="definition in this.response.definitions"  :key="definition.id" :definition="definition"></WordItem>
  </div>
</template>

<script>
import WordItem from './WordItem.vue'

export default {
  components: {
    WordItem
  },
  props: {
    response: Object
  }
}
</script>

<style>

</style>
