<template>
 <div class="todo-item"  > 
     <p>
        <!-- <el-checkbox label="iscompleted"></el-checkbox> -->
        <input type="checkbox" v-on:change="markComplete"  v-bind:class="{'is-complete':todo.completed}"/>
      {{todo.title}} <span v-bind:class="[todo.completed ? 'todoItemFinishText': 'todoItemProcessText']" >{{todo.completed ? 'finished': 'in process'}}</span> 
      <button @click="$emit('del-todo',todo.id)" class="del" >X</button>
      </p>
      </div> 
</template>
<script>
export default {
    name:"TodoItem",
    props:["todo"],
    methods:{
        markComplete(){
            this.todo.completed=!this.todo.completed;
            console.log(this.todo.completed);
        } 
    }
}
</script>
<style scoped>
 .todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }
  .is-complete {
    text-decoration: line-through;
    
  }
  .todoItemFinishText{
    color:green;
    font-weight: bold;
  }
  .todoItemProcessText{
   color:red;
    font-weight: bold;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>