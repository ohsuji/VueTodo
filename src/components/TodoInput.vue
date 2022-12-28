<template>
  <div class="inputBox shadow">
    <input type="text" 
    placeholder="Type what you have to do" 
    v-model="newTodoItem" 
    v-on:keyup.enter="addTodo">

    <span v-on:click="addTodo" class="addContainer">
      <i class="plus fa-solid fa-plus"></i>
    </span>

    <!-- 모달 팝업 설정 -->
    <AlertModal v-if="showModal">
      <h3 slot="header">
        <i class="fa-solid fa-star"></i>
        <i class="fa-solid fa-star"></i>
        <i class="fa-solid fa-star"></i>
      </h3>
      <span slot="footer">Type what you have to do
        <i class="closeModalBtn fa-solid fa-circle-xmark" v-on:click="showModal = false"></i>
      </span>
    </AlertModal>
  </div>
</template>

<script>
import AlertModal from "./AlertModal.vue";

export default {
  data() {
    return { 
      newTodoItem: "", 
      showModal: false, 
    };
  },
  methods: {
    addTodo() {
      // console.log('새로 입력한 값', this.newTodoItem);
      // localStorage.setItem(this.newTodoItem, this.newTodoItem);
      // setItem(Key, Value) 로컬스토리지에 데이터를 추가하는 API(함수)

      // 공백도 입력되는 상황을 막기위해
      if(this.newTodoItem !== ''){
        let value = this.newTodoItem && this.newTodoItem.trim();
        // localStorage.setItem(value, value); 직접 저장하지 않게
        // this.newTodoItem = '';  // 분리, 단일책임원칙
        this.$emit("addTodo", value);  // 상위 App.vue에 addTodo, value 전달
        this.clearInput(); 
      } else {  // 텍스트 미 입력시 모달팝업
        this.showModal = true;
      }
    },
    clearInput() {  
      // 인풋박스 입력 후 초기화
      this.newTodoItem = '';
    },
  },
  components: {
    AlertModal: AlertModal,
  }
};
</script>

<style scoped>
  .inputBox {
    background: #fff;
    height: 50px;
    line-height: 50px;
    border-radius: 10px;
  }
  span.addContainer {
    float: right;
    background: linear-gradient(to right, #add8e6, #72c2dd );
    width: 50px;
    border-radius: 0 10px 10px 0;
  }
  input {
    text-align: center;
    border: none;
    font-size: 1rem;
    width: calc(80% - 45px);
  }
  input:focus {
    outline: none;
  }
  i.plus {
    color: #fff;
    vertical-align: middel;
  }

  h3 {
    color: orange;
    font-size: 50px;

    margin: 0 0 1rem 0;
  }
  .closeModalBtn {
    color: lightcoral;
  }
</style>