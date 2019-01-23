# VueRouter

### router.js
```js
import Vue from 'vue'
import VueRouter from 'vue-router'

Vue.use(VueRouter)

const discounts = () => import('../pages/discounts.vue');
const shop = () => import('../pages/shop.vue');
const bbs = () => import('../pages/bbs.vue');

const xheader = () => import('../components/xheader.vue');
const uidlogin = () => import('../components/uidlogin.vue');
const phone = () => import('../components/phone.vue');



const routes = [{
//重定向
    path: '/',
    redirect: {
        path: '/index/discounts'
    }
},
{
    path: '/index',
    component: xheader,
    //二级路由
    children: [{
        path: 'discounts',
        name: 'discounts',
        component: discounts
    },
    {
        path: 'shop',
        name: 'shop',
        component: shop
    },
    {
        path: 'detail',
        name: 'detail',
        component: detail
    }]
}]


const router = new VueRouter({
//挂载配置
    routes,
    //新页面跳转到顶部
    scrollBehavior(to, from, savedPosition) {
        if (savedPosition) {
            return savedPosition
        } else {
            return { x: 0, y: 0 }
        }
    }
})

export default router;
```


### main.js
```js
import Vue from 'vue'
import App from './App.vue'
import router from './config/router.js'

new Vue({
    render: h => h(App),
    router
}).$mount('#app')
```
