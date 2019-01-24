# better-scroll简陋的例子

### 安装
```
cnpm i better-scroll --save
```
### 使用
```js
<template>
//必须有wrapper、content这两个class，且关系为父与子
  <div class="wrapper">
    <ul class="content">
      <li>
        ...
      </li>
      <h2 v-show="showLoading">加载中...</h2>
    </ul>
  </div>
</template>
<script>

//引入第三方模块
import BScroll from "better-scroll";

export default {
  data() {
    return {
      currentPage: 0,
      newgoodslist: [],
      scroll: "",
      //控制加载中是否显示
      showLoading: false
    };
  },
  methods: {
    async getNewGoods() {
      let newgoodslistdata = await this.$axios.get(
        "http://47.106.129.188:3000/findshops",
        {
          params: {
            page: this.currentPage++,
            find: {},
            qty: this.qty
          }
        }
      );
      this.newgoodslist = this.newgoodslist.concat(newgoodslistdata.data);
      this.showLoading = false;
      //因为dom节点更新了->刷新滚动条
      this.scroll.refresh();
    }
  },
  mounted() {
    this.getNewGoods();
    this.$nextTick(() => {
    //获取节点
      let wrapper = document.querySelector(".wrapper");
      // 传入设置 并实例化对象
      this.scroll = new BScroll(wrapper, {
      //上拉
        pullUpLoad: {
          threshold: 50,
          stop: 20
        },
      //下拉
        pullDownRefresh: {
          threshold: 50,
          stop: 20
        }
      });
      //上拉事件
      this.scroll.on("pullingUp", () => {
        //显示加载中
        this.showLoading = true;
        //发送ajax请求，获取更多数据
        this.getNewGoods();
        //事件结束必须执行
        this.scroll.finishPullUp();
      });
      //下拉事件
      this.scroll.on("pullingDown", () => {
        //事件结束必须执行
        this.scroll.finishPullDown();
      });
    });
  }
};
</script>
```
