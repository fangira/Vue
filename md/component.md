# component

### search.vue

```vue
<template>
  <div>
    <searchbar @toggle-searchC-component="toggleComponent"></searchbar>
    <component :is="currentComponent"></component>
  </div>
</template>

<script>
import searchbar from "../components/searchbar.vue";
import sort from "../components/sort.vue";
import searchres from "../components/searchres.vue";
export default {
  data() {
    return {
      currentComponent: sort,
      componentArr:[sort,searchres]
    };
  },
  methods: {
    toggleComponent(n){
      this.currentComponent = this.componentArr[n];
    }
  },
  components: {
    searchbar
  }
};
</script>
```

### searchbar.vue

```vue
<template>
  <div>
    <div id="searchbar">
      <div class="searchbar">
        <div class="search_l">
          <img src="../assets/search.svg">
          <input
            type="text"
            placeholder="搜索"
            @focus="toggleComponent(1)"
            @blur="toggleComponent(0)"
            @input="searchKey"
            v-model="keyWord"
          >
        </div>
        <span class="search_r" @click="backToLast">取消</span>
      </div>
    </div>
    <div class="empty"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      keyWord: ""
    };
  },
  methods: {
    toggleComponent(n) {
      this.$emit("toggle-searchC-component", n);
    },
    backToLast() {
      this.$router.go(-1);
    },
    searchKey() {
      this.$store.commit("setKeyWord", this.keyWord);
    }
  }
};
</script>
```
