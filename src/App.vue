<template>
  <div id="app">
    <!-- <img src="./assets/logo.png"> -->
    <Waterfall class="water"
     :minWidth="200"
     :items="items">
      <Item v-for="(item,index) in items" :item="item" :key="index"></Item>
    </Waterfall>
    <button @click="addItems">addItems</button>
  </div>
</template>

<script>
import Hello from './components/Hello'
import Waterfall from './components/waterfall.vue'
import Item from './components/item.vue'

export default {
  name: 'app',
  data() {
    return {
      items: [
        {
          content: 'aaaa'
        },
        {
          content: 'aaaa'
        },
        {
          content: 'aaaa'
        },
        {
          content: 'aaaa'
        },
        {
          content: 'aaaa'
        }
      ]
    }
  },
  methods: {
    addItems: function () {
      this._data.items.push({content: 'bbbbbbbbbbbbbbbbbbbbbbbbbbbbbb'})
    }
  },
  components: {
    Hello,
    Waterfall,
    Item
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.water{
  background-color: rgba(0,0,0,.2);
  position: relative;
  overflow: hidden;
}
</style>
