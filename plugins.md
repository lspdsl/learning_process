@代替./src

jsconfig.json

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"],
    }
  },
  "exclude": ["node_modules", "dist"]
}
```

# 1.datepicker

格式化日期

# 2.fullpage

# 3.lazyload

# 4.echarts

# 5.layui

# 6.swiper

# 7.element

# 8.vuex-persistedstate

让在vuex中管理的状态数据同时存储在本地，免去自己存储的环节

1. 安装

   ```bash
   npm i vuex-persistedstate
   ```

2. 创建vuexstore-----src/store/modules

   ```js
   // 用户模块
   export default {
     namespaced: true,
     state () {
       return {
         // 用户信息
         profile: {
           id: '',
           avatar: '',
           nickname: '',
           account: '',
           mobile: '',
           token: ''
         }
       }
     },
     mutations: {
       // 修改用户信息，payload就是用户信息对象
       setUser (state, payload) {
         state.profile = payload
       }
     }
   }
   ```

   ```js
   // 购物车状态
   export default {
     namespaced: true,
     state: () => {
       return {
         list: []
       }
     }
   }
   ```

   ```js
   // 分类模块
   export default {
     namespaced: true,
     state () {
       return {
         // 分类信息集合
         list: []
       }
     }
   }
   ```

   ```js
   // src/store/index.js
   import { createStore } from 'vuex'
   
   import user from './modules/user'
   import cart from './modules/cart'
   import cart from './modules/category'
   
   export default createStore({
     modules: {
       user,
       cart,
       category
     }
   })
   ```

3. 使用

   ```js
   import { createStore } from 'vuex'
   import createPersistate from "vuex-persistedstate"
   
   import user from './modules/user'
   import cart from './modules/cart'
   import cart from './modules/category'
   
   export default createStore({
     modules: {
       user,
       cart,
       category
     },
       plugins:[
           createPersistedstate({
               key:'token',
               paths:['user','cart']
           })
       ]
   })
   ```

    默认是存储在localStorage中

   key是存储数据的键名

   paths是存储state中的那些数据，如果是模块下具体的数据需要加上模块名称，如user.token

   修改state后触发才可以看到本地存储数据的的变化

# 9.qs

格式化参数

# 10.style-resources-loader

将less公用的变量和mixin自动注入到每个less文件或vue组件中的style标签中

1. 当前项目下安装

   ```bash
   vue add style-resources-loader
   ```

2. vue.config.js中添加配置

   ```js
   conso path=require('path')
   module.expots={
       pluginOptions:{
           'style-resourcesloader':{
               preProcessor:'less',
               patterns:[
                   path.join(__dirname,'./src/assets/styles/variables.less'),
                   path.join(__dirname,'./src/assets/styles/mixins.less')
               ]
           }
       }
   }
   ```

# 11.normalize

重置样式

1. 安装

   ```bash
   npm i normalize.css
   ```

2. main.js引入

   ```js
   import 'normalize.css'
   ```

   # 12.easy sass
   
   