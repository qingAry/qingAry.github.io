## vue简单搭建基本步骤：
**步骤一:**  [搭建vue环境](https://cli.vuejs.org/zh/guide/installation.html)

```
安装 npm install -g @vue/cli
查看 vue --version
创建项目 vue create project 
```

**步骤二:** 创建路由

```js
安装 npm install vue-router

配置路由：
pages -- vue模板
router -- js文件（index.js、routes.js）

/*index.js简单代码 开始*/

import Vue from "vue"
import VueRouter from 'vue-router'
import routes from './routes'

Vue.use(VueRouter);

export default new VueRouter({
    routes
})

/*index.js简单代码 结束*/

/*routes.js简单代码 开始*/

import List from "../pages/MyList"
export default [{
    name: "list",
    path: "/list",
    component: List
}]

/*routes.js简单代码 结束*/
```

**步骤三:**  创建仓库管理vuex

```js
安装 npm install vuex --save

配置vuex：
router -- js文件（index.js、testData.js）

/*index.js简单代码 开始*/
import Vue from 'vue'
import Vuex from 'vuex'
import testData from './testData'

Vue.use(Vuex);

export default new Vuex.Store({
    modules: {
        testData
    }
})
/*index.js简单代码 结束*/

/*testData.js简单代码 开始*/
const state = {
    name: 'haha'
}

const mutations = {}

const actions = {}

const getters = {}

export default {
    state,
    mutations,
    actions,
    getters
}
/*testData.js简单代码 结束*/
```



**步骤四 ：** main.js引入并使用

```js
/*别忘记最重要的一步，在main.js引入并使用*/

import Vue from 'vue'
import App from './App.vue'
import router from './router' /* 路由器 */
import store from './store' /* 仓库管理 */

Vue.config.productionTip = false

new Vue({
    render: h => h(App),
    router,
    store
}).$mount('#app')

/*别忘记最重要的一步，在main.js引入并使用*/
```



**步骤五 ：** vue.config.js配置

```js
const px2rem = require('postcss-px2rem')
const postcss = px2rem({
  remUnit: 75   //remUnit = 设计稿/等分数10， 网易严选首页750宽，正好相当于是设计稿宽度，所以值为750/10 = 75
})
module.exports = {
  lintOnSave:false,
  devServer:{
    open:true,
    proxy: {
      '/api': {
        target: 'http://localhost:3001',
        changeOrigin: true,
        'pathRewrite':{
          "^/api": ''
        }
      },
      '/yy':{
        target: 'https://***.com',//其他域名，你需要调用的数据
        changeOrigin: true,
        'pathRewrite':{
          "^/yy": ''
        }
      }
    }
   },
  css: {
    loaderOptions: {
      postcss: {
        plugins: [
          postcss
        ]
      }
    }
  }
}
```

