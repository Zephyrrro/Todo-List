<template>
  <div class="main">
    <h3>添加任务：</h3>
    <div class="submit">
      <input
        placeholder="回车添加+"
        v-model="todoItem.content"
        @keyup.enter="handleSubmit"
      >
    </div>
  </div>
</template>

<script>
// import { EventBus } from '../event-bus.js'
export default {
  props: ['list'],

  data () {
    return {
      todoItem: {
        content: '',
        isComplete: false
      },
    }
  },

  methods: {
    handleSubmit () {
      this.$emit('addItem', this.todoItem)
      this.todoItem.content = '';
    },
  }
}
</script>

<style scoped>
.main {
  width: 40vw;
  margin: 0 auto;
}

input {
  width: 35vw;
  height: 30px;
}

.submit {
  width: 35vw;
  margin: 20px auto;
}
</style>

