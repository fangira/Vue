# vue-lazyload

### 安装vue-lazyload插件
```
cnpm i vue-lazyload --save
```
### 在main.js引入
```js
import VueLazyload from 'vue-lazyload'

Vue.use(VueLazyload);
```
### 使用:所有图片属性:src换成v-lazy

```html
 <img v-lazy="newgoods.deal_pic">
```
