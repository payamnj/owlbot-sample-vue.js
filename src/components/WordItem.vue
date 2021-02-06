<template>
  <div class='definition-container'>
    <div class='image' v-show="imageUrl">
      <img :src="imageUrl" />
    </div>

    <div class="text-content">
      <span class='type' v-show="type">{{ type }}</span>
      <div>{{ definition.definition }}<span v-show="emoji">{{ emoji }}</span></div>
      <div class="example" v-show="example" v-html="example"></div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    definition: Object
  },
  computed: {
    imageUrl: function() {
      return this.definition['image_url'];
    },
    type: function() {
      return this.definition['type'];
    },
    example: function() {
      return this.definition['example'];
    },
    emoji: function() {
      return this.definition['emoji'];
    }
  }
}
</script>

<style scoped>
img {
  width: 45%;
  margin: 10px auto;
  border-radius: 50%;
}

.text-content {
  padding:  10px 0;
  text-align: left;
  font-size: 13px;
}

.type {
  display: inline-block;
  padding: 5px 0;
}

.example {
  padding: 10px 0;
  color: #8c8c8c;
}

.example::before {
  content: open-quote;
}
.example::after {
  content: close-quote;
}

.definition-container {
  border-bottom: solid 1px #cdcdcd;
  padding-bottom: 15px;
  margin-bottom: 10px;
}
</style>
