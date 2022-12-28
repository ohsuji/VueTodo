<template>
  <div class="clearContainer">
    <span @click="clearTodo" class="clearBtn">Clear All</span>
  </div>
</template>

<script>
export default {
  methods: {
    clearTodo() {
     // localStorage.clear();  로컬스토리지에서만 삭제
    this.$emit("removeAll"); 
    }
  }
}
</script>

<style scoped>
  .clearContainer {
    background: #5eaac4;
    border-radius: 10px;
    line-height: 50px;
    width: 120px;
    margin: 0 auto;
    color: #fff;
    font-weight: 600;
    font-size: 18px;
    cursor: pointer;
    transition: .4s;
  }
  .clearContainer:hover {
    color: lavender;
  }
  .clearBtn {
    display: block;
  }  
</style>