<template>
  <div class='mobile-ui-top' v-if="visible" id="app">
    <input v-model="word" maxlength="50" class='word-input' v-on:keyup.enter="callApi" />
    <div class="tab-switchers">
      <div class="btn" :class="{ active: isActive('u-i-view') }" @click="switchTo('u-i-view')">Web view</div>
      <div class="btn" :class="{ active: isActive('json-response') }" @click="switchTo('json-response')">Json response</div>
    </div>
      <component :is="currentTabComponent" :response="client.data" class='component-container' :style="{ 'max-height': displayHeight - 215 + 'px' }" v-show="!error"></component>
      <div class="error" v-show="error">{{ error }}</div>
  </div>
</template>

<script>
import OwlBot from 'owlbot-js';
import JsonResponse from './components/JsonResponse.vue'
import UIView from './components/UIView.vue'

export default {
  name: 'App',
  components: {
    JsonResponse,
    UIView
  },
  data: function() {
    return {
      visible: false,
      client: null,
      currentTabComponent: 'u-i-view',
      word: null,
      error: null
    };
  },
  props: {
    displayHeight: {
      type: Number,
      default: 600
    },
    initialWord: {
      type: String,
      default: 'pineapple'
    },
    token: {
      type: String,
      default: process.env.VUE_APP_TOKEN
    }
  },
  mounted: function() {
    this.visible = true;
    this.client = OwlBot(this.token);
    this.word = this.initialWord;
    this.callApi();
  },
  methods: {
    callApi: async function() {
      try {
        await this.client.define(this.word);
        this.error = null;
      } catch(err) {
        this.error = err;
      }
    },
    isActive: function(component) {
      if (component == this.currentTabComponent) {
        return true;
      } else {
        return false;
      }
    },
    switchTo: function(component) {
      this.currentTabComponent = component;
    }
  }
}
</script>

<style scoped>
.mobile-ui-top {
  padding-top: 85px;
  text-align: center;
}

.error {
  padding: 30px;
}

.word-input {
  border-radius: 5px;
  border: solid 1px #eee;
  height: 30px;
  padding: 2px 10px;
  font-size: 12px;
  width: 65%;
  background-color: #fbfafa;
}

.word-input:focus {
  border: solid 1px #badde0ba;
  outline: none;
}

.component-container {
  margin: 10px auto;
  width: 65%;
  overflow-y: scroll;
}

.btn {
  display: inline-block;
  border-radius: 4px;
  padding: 5px 5px;
  margin: 10px 5px 10px 0;
  color: #c22c7e;
  font-size: 11px;
  cursor: pointer;
  transition: 0.3s;
}

.btn:hover {
  background-color: #cd529529;
}

.tab-switchers {
  width: 65%;
  text-align: left;
  margin: 0 auto;
}

.btn.active {
  background-color: #c22c7ed1;
  color: white;
}
</style>
