# 1.开发环境--webpack反向代理

```js
module.export={
    devServer:{
        proxy:{
            '/api':{   // 开发中请求的地址
                target:'www.baidu.com', // 服务器所在地址,实际要请求的地址
                ws:true, // 代理websockets
                secure:false, // 代理https接口，true为选择
                changeOrigin:true,//true:开启跨域
                pathRewrite:{  // 跨域时重写请求地址
                    '^/api':'/'
                }
            }
        }
    }
}
```

# 2.生产环境--Nginx反向代理

```js
server{
    # 监听9099端口
    listen 9099;
    # 本地的域名是localhost
    server_name localhost;
    #凡是localhost:9099/api这个样子的，都转发到真正的服务端地址http://baidu.com
    location ^~ /api {
        proxy_pass http://baidu.com;
    }    
}
```

# 3.封装axios

基于axios封装一个请求工具，调用接口时使用

1. 安装

   ```bash
   npm i axios
   ```

2. 新建src/utils/request.js模块

   ```js
   // 1. 创建一个新的axios实例
   // 2. 请求拦截器，如果有token进行头部携带
   // 3. 响应拦截器：1. 剥离无效数据  2. 处理token失效
   // 4. 导出一个函数，调用当前的axsio实例发请求，返回值promise
   
   import axios from 'axios'
   // 格式化数据的第三方库
   import qs from 'qs'
   
   /*
   *环境配置，区分生产环境和开发环境
   */
   switch(process.env.NOOD_ENV){
       case "production": // 生产环境
           axios.defaults.baseUrl="生产环境地址";
           break;
       case "test": // 测试环境
           axios.defaults.baseUrl="测试环境地址";
           break;
       default:  // 开发环境
           axios.defaults.baseUrl="开发环境地址";
           break;
   }
   /*
   *设置超时时间，单位ms
   */
   axios.defaults.timeout=5000;
   
   /*
   *设置是否允许跨域和是否允许携带凭证，如果该设置为false，请求时不允许携带凭证
   */
   axios.defaults.withCredential=true;
   
   /*
   *设置请求头
   *	-设置请求传递数据的格式，通常要包含`x-www-form-urlencode`格式，改革书的数据通常为`xxx=xxx&yyy=yyy`,
   *	 这是为了post请求与get请求的格式相同
   */
   axios.defaults.headers["Content-Type"]="application/x-ww-form-urlencode";
   
   // 针对post请求设置数据格式，该方法transformRequest仅针对post请求有效
   // 使用qs库将传入的data数据转换为`x-ww-form-urlencode`格式
   // 如果服务器使用json格式，就不需要这样设置
   axios.defaults.transformRequest=data=>qs.stringify(data);
   
   // 请求拦截器
   axios.interceptors.request.use(config=>{
       return config
   },err=>{
       return Promise.reject(error)
   })
   
   // 响应拦截器
   axios.interceptors.response.use(res=>{
       return res.data
   })
   
   export default axios
   ```

   ```js
   import axios from 'axios'
   
   const serve=axios.create({
       baseUrl:baseUrl,
       timeout:5000;
   })
   
   // 请求拦截器
   instance.interceptors.request.use(config=>{
       return config
   })
   // 响应拦截器
   instance.interceptors.response.use(res=>res.data)
   
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

   ```js
   // 1. 创建一个新的axios实例
   // 2. 请求拦截器，如果有token进行头部携带
   // 3. 响应拦截器：1. 剥离无效数据  2. 处理token失效
   // 4. 导出一个函数，调用当前的axsio实例发请求，返回值promise
   
   import axios from 'axios'
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

   

