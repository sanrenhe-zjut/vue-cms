<template>
  <!-- 问题： 我们不知道什么时候能够拿到 max 值，但是，总归有一刻，会得到一个真正的 max 值 -->
  <!-- 我们可以 使用 watch 属性监听，来 监听 父组件传递过来的 max 值，不管 watch 会被触发几次，但是，最后一次，肯定是一个 合法的 max 数值 -->
  <div class="num-container">
    <div class="mui-numbox" data-numbox-min="1" style="height: 25px">
      <button class="mui-btn mui-btn-numbox-minus" type="button">-</button>
      <input
        id="test"
        class="mui-input-numbox"
        type="number"
        :value="initcount"
        @change="countChanged"
        ref="numbox"
        readonly
      />
      <button class="mui-btn mui-btn-numbox-plus" type="button">+</button>
    </div>
  </div>

  <!-- 分析： 子组件什么时候把 数据传递给父组件 -->
  <!--  -->
</template>

<script>
import mui from "../../lib/mui/js/mui.min.js";

export default {
  mounted() {
    // 初始化数字选择框组件
    mui(".mui-numbox").numbox();
    // console.log(this.initcount)
  },
  methods: {
    countChanged() {
      // 数量改变了
      // console.log(this.$refs.numbox.value);
      // 每当数量值改变， 则立即把最新的数量同步到 购物车的 store 中， 覆盖之前的值
      this.$store.commit("updateGoodsInfo", { id: this.goodsid, count: this.$refs.numbox.value })
    }
  },
  props: ["initcount", "goodsid"]
};
</script>

<style lang="scss">
.num-container {
  display: inline-block;
}
</style>