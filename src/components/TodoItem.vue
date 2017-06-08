<template>
  <li :style="{background: libg}"
      @mouseenter="handleStyle(true)" @mouseleave="handleStyle(false)">
    <label>
      <input type="checkbox" v-model="todo.isDone"/>
      <span>{{todo.title}}</span>
    </label>
    <button class="btn btn-danger" v-show="isShown" @click="deleteItem">删除</button>
  </li>
</template>

<script>
// 创建事件中心
//let Hub = new Vue()
export default {
  props:['todo','deleteTodo'],
  data () {
    return {
    	isShown:false,
    	 libg: '#fff'
    };
  },
  methods:{
  	handleStyle(isEnter){
  		// isEnter 判断传递的值
  		if(isEnter){
  			this.isShown = true
  			this.libg = '#ddd'
  		}else {
  			this.isShown = false
  			this.libg = '#fff'
  		}
  	},
  	deleteItem(){
  		// 触发父组件的方法  激发父组件的方法，第二个参数 传递参数
  		//this.$emit('deleteTodo', this.todo)
  	   this.deleteTodo(this.todo)
  	}
  }
};
</script>

<style lang="css" scoped>
li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    /*display: none;*/
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }
</style>