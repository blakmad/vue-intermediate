<template>
  <div Class="inputBox shadow">
    <!--v-model : 양방향 바인딩-->
    <input type="text" v-model="newTodoitem" v-on:keyup.enter="addTodo">
    <!--    <button @click="addTodo">추가</button>-->
    <span class="addContainer" v-on:click="addTodo">
      <i class="fa-regular fa-square-plus addBtn"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <!--
        여기에서 사용자 정의 컨텐츠를 사용하여 덮어 쓰일 수 있습니다
        기본 콘텐츠
      -->
      <h3 slot="header">
        경고
        <i class="closeModalBtn fa-solid fa-xmark" @click="showModal=false" ></i>
      </h3>
      <div slot="body">
        <input type="text" v-model="newTodoitem" v-on:keyup.enter="addTodo">
      </div>
      <span slot="footer">
        <button @click="showModal = false" >닫기</button>
      </span>

    </Modal>

  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data: function () {
    return {
      newTodoitem: "",
      showModal: false
    }
  },
  methods: {
    addTodo: function () {
      if (this.newTodoitem !== '') {
        // this.$emit('이벤트이름', 인자1, 인자2, ...);
        this.$emit('addTodoItem', this.newTodoitem);

        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput: function () {
      this.newTodoitem = '';

    }
  },
  components: {
    Modal : Modal
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

.closeModalBtn {
  color: #42b983;
}
</style>