<template>
  <div Class="inputBox shadow">
    <!--v-model : 양방향 바인딩-->
    <input type="text" v-model="newTodoitem" v-on:keyup.enter="addTodo">
    <!--    <button @click="addTodo">추가</button>-->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-regular fa-square-plus addBtn"></i>
    </span>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      newTodoitem: ""
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoitem !== '') {
        var obj = {completed: false, item: this.newTodoitem};
        localStorage.setItem(this.newTodoitem, JSON.stringify(obj));
        this.clearInput();
      }
    },
    clearInput: function () {
      this.newTodoitem = '';

    }
  }
}
</script>

<style scoped>
input:focus {
  outline: none;
}

.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}

.inputBox input {
  border-style: none;
  font-size: 0.9rem;

}

.addContainer {
  float: right;
  background: linear-gradient(to right, #fb648f, #8763FB);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-align: middle;
}
</style>