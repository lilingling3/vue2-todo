
<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <todo-header :addTodo="addTodo"></todo-header>
      <!--  @deleteTodo 传递给子组件 -->
      <todo-main :todos="todos" :deleteTodo="deleteTodo"></todo-main>
      <todo-footer :todos="todos" :updateTodos="updateTodos"
           :deleteDone="deleteDone"></todo-footer>
    </div>
  </div>
</template>


<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoFooter from './components/TodoFooter.vue'
import TodoMain  from './components/TodoMain.vue'
import storageUtil from './util/storageUtil'
export default {
  data () {
    return {
    	todos:[]
    };
  },
  created(){
  	//this.todos = [{isDone: false, title: '吃饭'}, {isDone: true, title: '睡觉'}]
    // Hub.on('deleteTodo',(todo) =>{
    //   const index = this.todos.indexOf(todo);
    //   if(confirm(`确认删除${todo.title}`)){
    //     this.todos.splice(index,1)
    //   }
    // })
    // 利用本地存储 异步读取数据
     this.todos = storageUtil.fetch()
  },
  methods:{
  	// 添加todo
  	addTodo(todo){
  		this.todos.unshift(todo)
  	},
  	// 删除todo
  	deleteTodo(todo){
  		const index = this.todos.indexOf(todo);
      if(confirm(`确认删除${todo.title}`)){
        this.todos.splice(index,1)
      }
  	
  	},
  	// 删除完成的todo
  	deleteDone(){
  		this.todos = this.todos.filter(todo =>!todo.isDone)
  	},
  	// 设置todo 为指定状态
  	updateTodos(isDone){
  		this.todos.forEach(todo =>todo.isDone = isDone)
  	}

  },
  watch:{// 深度监视数据变化
  	todos:{
      handler: storageUtil.save,
  		deep:true
  	}
  },
  events:{// 自定义事件

  },
  components:{TodoHeader, TodoFooter, TodoMain}
};
</script>

<style lang="css" scoped>
.todo-container {
    width: 600px;
    margin: 0 auto;
  }

  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>