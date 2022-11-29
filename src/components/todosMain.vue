<template>
  <!-- 主体部分 -->
  <section class="main">
    <input
      v-model="checkAll"
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
    />
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
      <!-- <li class="completed">
        <div class="view">
          <input class="toggle" type="checkbox" checked />
          <label>读万卷书</label>
          <button class="destroy"></button>
        </div>
      </li> -->
      <li :class="{ completed: item.flag }" v-for="item in data" :key="item.id">
        <div class="view">
          <!-- 不能直接用v-model绑定,当修改值时同时修改了父组件中数据值,违反了组件中单项数据流规则,所有要用动态属性值checked绑定 -->
          <input
            :checked="item.flag"
            @change="checkVal(item.id)"
            class="toggle"
            type="checkbox"
          />
          <label>{{ item.name }}</label>
          <button class="destroy" @click="del(item.id)"></button>
        </div>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  props: {
    data: Array,
  },
  methods: {
    //删除任务
    del(id) {
      this.$emit("delName", id);
    },
    //修改值
    checkVal(id) {
      this.$emit("checkval", id);
    },
  },
  computed: {
    //全选按钮
    checkAll: {
      get() {
        //点击每一个复选框按钮,都选中了才让上面全选按钮选中
        return this.data.every((item) => item.flag === true);
      },
      set(val) {
        console.log(val, 123);
        this.$emit("changeAll", val);
      },
    },
  },
};
</script>

<style>
</style>