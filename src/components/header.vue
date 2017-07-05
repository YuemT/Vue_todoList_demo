<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认"
      v-model="inputTodo" @keyup.enter="addTodo"/>
  </div>
</template>

<script>
    export default{
        //声明接收属性
      props:{
          add:Function,
          required:true
      },
      //初始化数据
      data(){
          return{
              inputTodo:''
          }
      },
      methods:{
          addTodo(){
            //判断输入的值是否合法
            var inputTodo = this.inputTodo.trim()
            if(!inputTodo){
                return
            }
            //获取input输入的值,创建一个todo对象
            var todo = {
                name: this.inputTodo,
                complete: false
            }
            //添加todo到todos
            //注意数据定义在哪个组件，修改数据的方法就在哪个组件
            this.add(todo)
            //清空输入
            this.inputTodo = ''
          }
      }
    }
</script>

<style>
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>
