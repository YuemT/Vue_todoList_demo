<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <todo-header :add="add"></todo-header>
      <list :todos="todos" :remove="remove"></list>
      <todo-footer :todos="todos" :remove-selected="removeSelected" :select-all-todos="selectAllTodos"></todo-footer>
    </div>
  </div>
</template>

<script>
  import list from './list.vue'
  import header from './header.vue'
  import footer from './footer.vue'
  import storageUtils from '../util/localStorageUtil'

  export default{
    data(){
      return {
        todos:[]
      }
    },
    created(){
      //模拟从后台获取数据
      setTimeout(()=>{
          this.todos = storageUtils.readTodos()
      },1000)
    },
    methods:{
      add (todo) {
          this.todos.unshift(todo)
      },
      remove(index){
          this.todos.splice(index,1)
      },
      removeSelected(){
          //过滤留下未选中的
        this.todos = this.todos.filter(todo => !todo.complete)
      },
      selectAllTodos(isCheck){
          this.todos.forEach(todo=>{
              todo.complete = isCheck
          })
      }
    },
    watch:{
      todos:{
          deep:true,
//          handler(newTodos){
//            //保存
//            storageUtils.saveTodos(newTodos)
//          }
          handler:storageUtils.saveTodos
      }
    },
    components:{
        'todo-header':header,
        list,
        'todo-footer':footer
    }
  }
</script>

<style>
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
