# props
一般在父向子组件通讯的时候使用

### 父组件.vue
```vue
<template>
  <div>
    <xheadersecond title="今日加倍返利" hasMore=1 imgurl="./xxx.svg"></xheadersecond>
  </div>
</template>
```

### 子组件.vue

```vue

<template>
  <div>
    <div class="wt">
      <img :src="imgurl" />
      <h3 class="wt__title wt__title--icon-title" v-text="title"></h3>
      <router-link to="/index/moreshop" href="/store/double-rebate" class="wt__more" v-text="hasMore?'查看更多':''"></router-link>  
    </div>
  </div>
</template>
<script>

export default {
  props:[
    'title',
    'hasMore',
    'imgurl'
  ]
};
</script>
```
