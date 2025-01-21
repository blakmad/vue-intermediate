<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input v-on:addTodoItem="addOneItem"></todo-input>
    <todo-list v-bind:propsdata="todoItems" v-on:removeItem="removeOneItem" v-on:toggleItem="toggleOneItem"></todo-list>
    <todo-footer v-on:clearAll="clearAllItems"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoFooter from './components/TodoFooter.vue'
import TodoList from './components/TodoList.vue'


export default {

  data: function () {
    return {
      todoItems: []
    }
  },
  created: function () {// 컴포넌트가 생성되면 실행되는 함수
    if (localStorage.length > 0) {
      for (var i = 0; i < localStorage.length; i++) {
        if (localStorage.key(i) !== 'loglevel:webpack-dev-server') {
          this.todoItems.push(JSON.parse(localStorage.getItem(localStorage.key(i))));
        }
      }
    }
  },
  methods:{
    addOneItem:function(todoItem){
      var obj = {completed: false, item: todoItem};
      localStorage.setItem(todoItem, JSON.stringify(obj));
      this.todoItems.push(obj);//push : 배열에서 배열요소 추가.
    },
    removeOneItem:function(todoItem, index){

      localStorage.removeItem(todoItem.item);
      this.todoItems.splice(index, 1);  //  splice(index, 1) 배열의 요소를 삭제한다.
    },
    toggleOneItem:function(todoItem, index){
      // todoItem.completed = !todoItem.completed;
      this.todoItems[index].completed = !this.todoItems[index].completed;
      localStorage.removeItem(todoItem.item);
      localStorage.setItem(todoItem.item, JSON.stringify(todoItem));
    },
    clearAllItems: function(){
      localStorage.clear();
      this.todoItems = [];
    }
  },
  components: {
    'todo-header': TodoHeader,
    'todo-input': TodoInput,
    'todo-footer': TodoFooter,
    'todo-list': TodoList
  }
}
</script>

<style>

body {
  text-align: center;
  background-color: #F6F6F6;
}

input {
  border-style: groove;

}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
}


</style>
