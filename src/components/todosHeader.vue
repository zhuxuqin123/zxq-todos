<template>
  <!-- 头部部分 -->
  <header class="header">
    <h1>todos</h1>
    <input
      v-model="msg"
      @keyup.enter="add"
      class="new-todo"
      placeholder="请输入任务名称"
      autofocus
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      msg: "",
    };
  },
  methods: {
    //键盘弹起事件  添加任务
    add() {
      this.$emit("addName", this.msg);
      this.msg = "";
    },
  },
};
</script>

<style>
</style>