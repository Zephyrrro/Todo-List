<template>
  <div>
    <Header></Header>
    <add-item @addItem="handleAdd"></add-item>
    <!-- <dataFilter
      :list="list"
      :visibility="visibility"
      :hash="hash"
    ></dataFilter> -->
    <div class="display">
      <h3>任务列表<span>（双击修改）</span></h3>
      <ul>
        <p v-if="isListEmpty">还未添加任何任务</p>
        <displayItem
          v-for="(item, index) in list"
          :key="index"
          :item="item"
          :index="index"
          @delete="handleDelete"
          @modify="handleModify"
        ></displayItem>
      </ul>
    </div>
  </div>
</template>

<script>
import DisplayItem from './components/DisplayItem'
import Header from './components/Header'
import AddItem from './components/AddItem'
// import DataFilter from './components/DataFilter'

export default {
  components: {
    'displayItem': DisplayItem,
    'Header': Header,
    'add-item': AddItem,
    // 'dataFilter': DataFilter
  },
  data () {
    return {
      isListEmpty: true,
      list: [],
      checkAllSpace: new RegExp(/^[ ]*$/),
      newContent: '',
      visibility: '#all',
      hash: window.location.hash.slice(1)
    }
  },
  methods: {
    handleAdd (todoItem) {
      if (this.checkAllSpace.test(todoItem.content)) {
        alert('Do not enter any empty content!');
      } else {
        this.list.push(JSON.parse(JSON.stringify(todoItem)));
        this.isListEmpty = false;
      }
    },
    handleDelete (index) {
      if (confirm('确认删除？') === true) {
        this.list.splice(index, 1);
      }
    },
    handleModify (index) {
      this.newContent = prompt('New content:');
      if (this.newContent === null) {
        return;
      } else if (this.checkAllSpace.test(this.newContent)) {
        alert('Do not enter any empty content!');
      } else {
        this.$set(this.list[index], 'content', this.newContent);
      }
    }
  },
}
</script>

<style scoped>
* {
  padding: 0;
  margin: 0;
}
span {
  font-size: 12px;
}
p {
  height: 40px;
  color: gray;
  line-height: 40px;
}
.display {
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-top: 30px;
}
ul {
  width: 40vw;
  background-color: #fff;
}
</style>
