# 模块化的几种方法
1. ## .vue组件化 (没有脚手架就看我吧)
    + index.js
    ```js
    import Vue from 'vue'
    import axios from 'axios'
    import Xheader from './components/Xheader.vue'
    import Xsearch from './components/Xsearch.vue'
    import Xpanel from './components/Xpanel.vue'
    import Xfooter from './components/Xfooter.vue'
    Vue.prototype.$axios = axios;
    // 引入微信样式
    import 'weui'
    new Vue({
        el: "#demo",
        data: {},
        template: `
            <div>
                <Xheader></Xheader>
                <Xsearch></Xsearch>
                <Xpanel></Xpanel>
                <Xfooter></Xfooter>
            </div>
        `,
        // 等价于全局注册
        components:{
            Xheader,
            Xsearch,
            Xpanel,
            Xfooter
        }
    })
    ```
    + Xheader.vue
    ```vue
    <template>
      <header v-text="title"></header>
    </template>
    
    <script>
    export default {
      data() {
        return {
          title: "今日头条"
        };
      }
    };
    </script>
    
    <style scoped>
    header {
      height: 50px;
      width: 100%;
      background-color: red;
    }
    </style>
    ```
2. ## 超级细分组件化（大项目，大公司，细分公）
   + index.js
   ```js
   import Xheader from './components/Xheader/Xheader.js'
   
   new Vue({
    el: "#demo",
    template: `
        <div>
            <Xheader></Xheader>
        </div>
    `
    })
   ```
   + Xheader.js  Xheader文件夹下有.css .html .js
   ```js
    import Vue from 'vue'
    // css
    import './Xheader.css'
    let Xheader = Vue.component("Xheader", {
        // html
        // 需要配置html-loader
        template: require('./Xheader.html')
    })
    export default Xheader
   ```
   + 
   + 
3. ## 外部定义注册全局组件（远古级别）
   + xheader.js
    ```js
    Vue.component("xheader", {
        template: `
           <div>header</div>
        `,
        data(){
            return {
                news: []
            }
        },
        methods: {
            async loadMore() {
            }
        },
        created() {
            this.loadMore()
        }
    })
    ```
  + index.html 在主组件所在的html文件 用script标签引入
  ```html
  <div id="app">
        <Xheader></Xheader>
  </div>
  <script src="../javascripts/components/Xheader.js"></script>
  ```
