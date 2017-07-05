<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" v-model="allComplete"/>
    </label>
    <span>
          <span>已完成{{completeTodo}}</span> / 全部{{todos.length}}
        </span>
    <button class="btn btn-danger" v-show="completeTodo>0" @click="removeSelected">清除已完成任务</button>
  </div>
</template>

<script>
    export default{
      props:['todos','removeSelected','selectAllTodos'],
      computed:{
        //计算完成的todo的数量
        completeTodo(){
//          //reduce的原理
//          var total = 0
//          for(var i = 0; i < todos.length; i++){
//              var todo = todos[i];
////              if(todo.complete){
////                total++
////              }
//            total += todo.complete ? 1 : 0
//          }
          //filter 会返回一个新数组
          //return this.todos.filter(todo => todo.complete).length
          return this.todos.reduce((preTotal,todo)=>{
            return preTotal + (todo.complete?1:0)//最后遍历的元素返回的结果就是reduce的返回值
          },0)
        },
        allComplete:{
            get(){
              return this.completeTodo === this.todos.length && this.completeTodo != 0
            },
            set(value){
              //根据新值设置全选或者全不选
              this.selectAllTodos(value)
            }
        }
      }
    }
</script>

<style>
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }

</style>
