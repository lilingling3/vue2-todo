<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="isAllDone"/>
    </label>
    <span>
      <span>已完成{{doneCount}}</span> / 全部{{totalCount}}
    </span>
    <button class="btn btn-danger" @click="deleteDone">清除已完成任务</button>
  </div>
</template>

<script>
export default {
	// props data computed 中都是可以在页面中直接使用的属性
  props:['todos', 'deleteDone', 'updateTodos'],
  data () {
	 return {

	 };
  },
  computed:{
  	isAllDone:{
  		// 所有都完成 (todos 数量大于0；没有完成的数量为0；所有都是已经完成的)
  		get(){
  		  return this.todos.filter(todo => !todo.isDone).length ===0 && this.todos.length >0;
  		},
  		set(val){
  			this.updateTodos(val)
  		}
  	},
  	doneCount(){
  		return this.todos.filter(todo =>todo.isDone).length;
  	},
  	totalCount(){
  		return this.todos.length;
  	}
  }
};
</script>

<style lang="css" scoped>
</style>