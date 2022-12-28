<template>
  <div>
    <TransitionGroup name="list" tag="ul">
      <!-- vue 2.2.0 이상에서는 key값 필수 -->
      <li v-for="(todoItem, index) in propsdata" :key="index" class="shadow">
        <i class="checkBtn fa-solid fa-check"></i>
        <span class="text">{{todoItem}}</span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)">
          <i class="fa-solid fa-trash-can"></i>
        </span>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: ["propsdata"], 
  /* App.vue로 이동
  data (){
    return { todoItems: [] }; // 스토리지 내용을 집어 넣을 배열 선언
  },
  */

  /* App.vue로 이동
  created: function() {
    if(localStorage.length > 0) {
      for(let i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  */
  methods: {
    removeTodo: function(todoItem, index) {
      // console.log("key : " + index + ",value: " + todoItem);
      this.$emit('removeTodo', todoItem, index);

      /* App.vue로 가져감 
      localStorage.removeItem(todoItem);  // 로컬스토리지에서 삭제
      this.todoItems.splice(index, 1);
      .splice() -  배열 특정 항목을 제거 */
    }
  }
};
</script>

<style scoped>
  ul {
    list-style: none;
    padding-left: 0;
  }
  li {
    display: flex;
    justify-content: space-between;
    background: #fff;
    height: 50px;
    line-height: 50px;
    margin: 8px 0;
    padding-left: 20px;
    border-radius: 10px;
    text-align: left;
  }
  .checkBtn {
    line-height: 50px;
    margin-right: 7px;
    color: lightcoral;
  }
  .text {
    width: 80%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .removeBtn {
    color: burlywood;
    width: 50px;
    text-align: center;
    cursor: pointer;
  }
  .list-enter-active, .list-leave-active {
    transition: all 0.5s ease;
  }
  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(10px);
  }
</style>