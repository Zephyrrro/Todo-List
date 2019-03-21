<template>
  <div>
    <span>{{uncompletedNum}}个任务尚未完成</span>
    <a
      :class="{active:visibility!=='unCompleted'&&visibility!=='completed'}"
      href="#all"
    >所有任务</a>
    <a
      :class="{active:visibility==='unCompleted'}"
      href="#unCompleted"
    >未完成的任务</a>
    <a
      :class="{active:visibility==='completed'}"
      href="#completed"
    >完成的任务</a>
  </div>
</template>

<script>
export default {
  props: ['list', 'visibility', 'hash'],
  computed: {
    uncompletedNum () {
      return this.list.filter(function (item) {
        return !item.isComplete;
      }).length
    },
  },
  watch: {
    list: {
      filterData () {
        let filter = {
          all: function (list) {
            return list;
          },
          completed: function (list) {
            return list.filter(function (item) {
              return item.isComplete;
            })
          },
          unCompleted: function (list) {
            return list.filter(function (item) {
              return !item.isComplete;
            })
          }
        }
        return filter[this.visibility] ? filter[this.visibility](this.list) : this.list;
      }
    },
  }
}
</script>

<style scoped>
</style>
