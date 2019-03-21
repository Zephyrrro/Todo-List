<template>
  <div class="main">
    <input
      type="checkbox"
      v-model="item.isComplete"
    >
    <li
      class="item"
      :class="{'completed':item.isComplete, }"
      @dblclick="commitMod"
    >{{item.content}}
      <button @click="commitDel">Delete</button>
    </li>
  </div>
</template>

<script>
// import { EventBus } from '../event-bus.js'
export default {
  props: ['item', 'index'],
  methods: {
    commitDel () {
      this.$emit('delete', this.index);
    },
    commitMod () {
      this.$emit('modify', this.index);
    }
  },
}
</script>

<style scoped>
input {
  width: 18px;
  height: 18px;
  margin: 0 15px;
  outline: none;
}
.item {
  cursor: pointer;
  list-style: none;
  width: calc(40vw - 30px);
}
.item button {
  display: none;
  float: right;
  margin-right: 20px;
  width: 60px;
  background: linear-gradient(to right, red, pink);
}
.item:hover button {
  display: block;
}
.completed {
  text-decoration: line-through;
  color: #d9d9d9;
}
button {
  background-color: #ebebeb;
  height: 25px;
  border: 1px solid transparent;
  border-radius: 15px;
  outline: none;
  box-shadow: 1px 4px 4px gray;
}
button:active {
  transform: translateY(3px);
  box-shadow: 1px 1px 4px gray;
}
.main {
  /* width: 50vw; */
  height: 40px;
  border-bottom: 1px solid #ededed;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
