<template>
  <ul class="todo-main">
  <!-- 默认v-for 需要 :key="item.id"  -->
    <todo-item v-for="todo in todos" :todo="todo" :key="todo.id" :deleteTodo='deleteTodo'></todo-item>
  </ul>
</template>

<script>
import TodoItem from './TodoItem.vue'
export default {
  props:['todos','deleteTodo'],
  components: {TodoItem}
};
</script>

<style lang="css" scoped>
.todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }
</style>