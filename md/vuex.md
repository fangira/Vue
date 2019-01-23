# Vuex

### main.js

```js
import Vue from 'vue'
import App from './App.vue'
import store from './config/store.js'

new Vue({
    render: h => h(App),
    store
}).$mount('#app')
```

### store.js

```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

const store = new Vuex.Store({
    //设置储存值
    state: {
        curGoods: {},
        keyWord: ''
    },
    //用this.$store.commit('setCurGoods') 触发mutations内的函数
    mutations: {
        setCurGoods(state, newGoods) {
            state.curGoods = newGoods;
            localStorage.setItem('curGoods', JSON.stringify(newGoods));
        },
        setKeyWord(state, newWord) {
            state.keyWord = newWord;
        }
    },
    //用this.$store.getters.getCurGoods 来获取getters内的返回值
    getters: {
        getCurGoods(state) {
            if (state.curGoods == {}) {
                return state.curGoods;
            } else {
                return JSON.parse(localStorage.getItem('curGoods'));
            }
        },
        getKeyWord(state) {
            return state.keyWord;
        }
    },
    //一般mutations就够用了，actions用来处理异步操作
    //用this.$store.dispatch('doSetCurGoods') 来触发
    actions: {
    doSetCurGoods (context) {
    //触发actions后，触发mutations的函数
      context.commit('setCurGoods')
    }
  }
})


export default store;
```
