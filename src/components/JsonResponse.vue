<template>
  <vue-json-pretty
    class="mobile-code"
    :path="'res'"
    :data="response">
  </vue-json-pretty>
</template>

<script>
import VueJsonPretty from 'vue-json-pretty'
import 'vue-json-pretty/lib/styles.css'

export default {
  components: {
    VueJsonPretty,
  },
  props: {
    response: Object
  },
  methods: {
    stringify: function(response) {
      return JSON.stringify(response);
    }
  }
}
</script>

<style scoped>
.mobile-code {
  background: #efefefc2;
  text-align: left;
  padding: 10px;
  border-radius: 5px;
  font-size: 12px;
  border: solid 1px #d2d2d2;
  word-wrap: break-word;
}

</style>
