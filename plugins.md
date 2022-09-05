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

# 9.axios封装

基于axios封装一个请求工具，调用接口时使用

1. 安装
   ```bash
   npm i axios
   ```

2. 新建src/utils/request.js模块

   ```js
   / 1. 创建一个新的axios实例
   // 2. 请求拦截器，如果有token进行头部携带
   // 3. 响应拦截器：1. 剥离无效数据  2. 处理token失效
   // 4. 导出一个函数，调用当前的axsio实例发请求，返回值promise
   
   import axios from 'axios'
   import store from '@/store'
   import router from '@/router'
   
   // 导出基准地址，原因：其他地方不是通过axios发请求的地方用上基准地址
   export const baseURL = 'http://pcapi-xiaotuxian-front-devtest.itheima.net/'
   const instance = axios.create({
     // axios 的一些配置，baseURL  timeout
     baseURL,
     timeout: 5000
   })
   
   instance.interceptors.request.use(config => {
     // 拦截业务逻辑
     // 进行请求配置的修改
     // 如果本地又token就在头部携带
     // 1. 获取用户信息对象
     const { profile } = store.state.user
     // 2. 判断是否有token
     if (profile.token) {
       // 3. 设置token
       config.headers.Authorization = `Bearer ${profile.token}`
     }
     return config
   }, err => {
     return Promise.reject(err)
   })
   
   // res => res.data  取出data数据，将来调用接口的时候直接拿到的就是后台的数据
   instance.interceptors.response.use(res => res.data, err => {
     // 401 状态码，进入该函数
     if (err.response && err.response.status === 401) {
       // 1. 清空无效用户信息
       // 2. 跳转到登录页
       // 3. 跳转需要传参（当前路由地址）给登录页码
       store.commit('user/setUser', {})
       // 当前路由地址
       // 组件里头：`/user?a=10` $route.path === /user  $route.fullPath === /user?a=10
       // js模块中：router.currentRoute.value.fullPath 就是当前路由地址，router.currentRoute 是ref响应式数据
       const fullPath = encodeURIComponent(router.currentRoute.value.fullPath)
       // encodeURIComponent 转换uri编码，防止解析地址出问题
       router.push('/login?redirectUrl=' + fullPath)
     }
     return Promise.reject(err)
   })
   
   // 请求工具函数
   export default (url, method, submitData) => {
     // 负责发请求：请求地址，请求方式，提交的数据
     return instance({
       url,
       method,
       // 1. 如果是get请求  需要使用params来传递submitData   ?a=10&c=10
       // 2. 如果不是get请求  需要使用data来传递submitData   请求体传参
       // [] 设置一个动态的key, 写js表达式，js表达式的执行结果当作KEY
       // method参数：get,Get,GET  转换成小写再来判断
       // 在对象，['params']:submitData ===== params:submitData 这样理解
       [method.toLowerCase() === 'get' ? 'params' : 'data']: submitData
     })
   }
   
   ```

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

   