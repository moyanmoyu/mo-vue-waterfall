# vue-waterfall

> 根据我的博客写的瀑布流样式
> 博客地址：www.moyanmoyu.me

## 使用方法
引用
```
import Waterfall from './components/waterfall.vue'
```
使用
```
<Waterfall class="water"
   :minWidth="200"
   :items="items">
   <Item v-for="(item,index) in items" :item="item" :key="index"></Item>
</Waterfall>
```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).


