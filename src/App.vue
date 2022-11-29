<template>
  <section class="todoapp">
    <!-- 使用组件 -->
    <todosHeader @addName="handleAdd"></todosHeader>
    <todosMain
      :data="showList"
      @delName="handleDel"
      @checkval="handleCheckval"
      @changeAll="changeAll"
    ></todosMain>
    <todosFooter :data="list" :type="type" @tyPE="handleType"></todosFooter>
  </section>
</template>

<script>
//导入组件
import todosHeader from "./components/todosHeader.vue";
import todosMain from "./components/todosMain.vue";
import todosFooter from "./components/todosFooter.vue";
export default {
  //注册组件
  components: {
    todosHeader,
    todosMain,
    todosFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("data")) || [
        { id: 1, name: "吃饭", flag: true },
        { id: 2, name: "睡觉", flag: false },
        { id: 3, name: "玩游戏", flag: true },
        { id: 4, name: "逛街", flag: false },
      ],
      type: "all",
    };
  },
  methods: {
    //处理子组件传过来的添加数据
    handleAdd(value) {
      this.list.unshift({ id: this.list.length + 1, name: value, flag: false });
    },
    //处理子组件传递过来的删除数据
    handleDel(value) {
      this.list = this.list.filter((item) => item.id !== value);
    },
    //编辑修改数据
    handleCheckval(id) {
      this.list.forEach((item) => {
        if (item.id === id) {
          item.flag = !item.flag;
        }
      });
    },
    //点击选中全部,进行中,已完成,高亮
    handleType(type) {
      this.type = type;
    },
    //处理子组件传过来的点击全选,下面复选框全选中
    changeAll(val) {
      this.list.forEach((item) => {
        item.flag = val;
      });
    },
  },
  computed: {
    showList() {
      if (this.type === "all") {
        return this.list;
      } else if (this.type === "active") {
        return this.list.filter((item) => item.flag === false);
      } else if (this.type === "computed") {
        return this.list.filter((item) => item.flag === true);
      } else {
        return this.list.filter((item) => item.flag === false);
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler(newVal) {
        localStorage.setItem("data", JSON.stringify(newVal));
      },
    },
  },
};
</script>

<style>
</style>
