<template>
  <!-- 底部部分 -->
  <footer class="footer" v-if="data.length">
    <span class="todo-count"
      ><strong>{{ total }}</strong
      >剩余</span
    >
    <ul class="filters">
      <li>
        <a
          @click="filter('all')"
          :class="{ selected: type === 'all' }"
          href="#/"
          >全部</a
        >
      </li>
      <li>
        <a
          @click="filter('active')"
          :class="{ selected: type === 'active' }"
          href="#/active"
          >进行中</a
        >
      </li>
      <li>
        <a
          href="#/completed"
          @click="filter('computed')"
          :class="{ selected: type === 'computed' }"
          >已完成</a
        >
      </li>
    </ul>
    <button
      v-if="isShow"
      @click="filter('clear')"
      :class="{ selected: type === 'clear' }"
      class="clear-completed"
    >
      清除已完成
    </button>
  </footer>
</template>

<script>
export default {
  props: {
    data: {
      type: Array,
      required: true,
    },
    type: {
      type: String,
    },
  },

  methods: {
    // 点击全部,进行中,已完成
    filter(type) {
      this.$emit("tyPE", type);
    },
    //点击清除已完成
    destroy() {
      this.$emit("destroy");
    },
  },
  computed: {
    //还剩几条
    total() {
      return this.data.filter((item) => item.flag === false).length;
    },
    //控制清除按钮已完成是否显示
    isShow() {
      return this.data.some((item) => item.flag === true);
    },
  },
};
</script>

<style>
</style>