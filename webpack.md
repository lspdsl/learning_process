

# yarn

```bash
# 1. 初始化, 得到package.json文件(终端路径所在文件夹下)
yarn init

# 2. 添加依赖(下包)
# 命令: yarn add [package]
# 命令: yarn add [package]@[version]
yarn add jquery
yarn add jquery@3.5.1

# 3. 移除包
# 命令: yarn remove [package]
yarn remove jquery
             
# 4. 安装项目全部依赖(一般拿到别人的项目时, 缺少node_modules)          
yarn
# 会根据当前项目package.json记录的包名和版本, 全部下载到当前工程中

# 5. 全局
# 安装: yarn global add [package]
# 卸载: yarn global remove [package]
# 注意: global一定在add左边
yarn global add @vue/cli
# 如何使用, 为明天学习vue做铺垫

# 6.更改镜像源
yarn config set registry=
yrm use 镜像源

# 7.查看所有可用镜像源
yrm ls

```

# webpack使用步骤

1.初始化包环境

```bash
yarn init
```

2.下载webpack模块

```bash
yarn add webpack webpack-cli -D
```

3.package.json设置自定义命令

```json
"scripts":{
    "build":"webpack"
}
```

添加命令后，控制端使用webpack build命令即可打包当前目录下的文件,文件修改后，再次使用webpack build即可重新打包

4.创建入口

webpack入口默认是/src/index.js，在入口js文件中使用import导入需要打包到一起的模块

5.执行webpack build打包命令

6.打包文件

生成出口，默认在/dist/main.js

# webpack自定义入口和出口

1.配置webpack,创建入口

创建/src/main.js作为webpack打包的入口

2.创建webpack.config.js，配置webpack

```js
const path = require('path');

module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js',
  },
};
```

entry:峪口文件目录

output.path:出口文件存放目录

output.filename:出口文件的文件名

3.修改package.json

```json
"scripts":{
    "build":"webpack"
}
```

# 自动生成html文件

使用 html-webpack-plugin插件, 让webpack打包后生成html文件并自动引入打包后的js

1.下载html-webpack-plugin插件

```bash
yarn add html-webpack-plugin -D
```

2.package.config.js添加配置

```js
module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js',
    },
    plugins: [new HtmlWebpackPlugin({  //   plugins插件配置
        template:'./public/index.html'//    webpack使用插件时,用来做模板的html的位置,生成html文件
    })],
}
```

生成的html文件一同放在dist目录下

3.执行yarn build命令

将文件打包的同时自动生产一个html文件,与bundke.js共同存放在dist目录下

# webpack打包css文件

Webpack 支持使用 [loader](https://webpack.docschina.org/concepts/loaders) 对文件进行预处理。你可以构建包括 JavaScript 在内的任何静态资源。并且可以使用 Node.js 轻松编写自己的 loader。

css-loader:webpack解析css文件，把css代码一起打包进js文件中

style-loader:css代码插入到DOM上(style标签)

1.下载css-loader和style-loader

```bash
yarn add webpack webpack-cli -D
yarn add css-loader style-loader -D
```

2.配置package.json

```bash
"scripts":{
    "build":"webpack"
}
```

3.入口中导入css文件

```js
//  引入css文件
import './css/index.css'
```

4.package.config.js添加配置

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js',
    },
    plugins: [new HtmlWebpackPlugin({  //   plugins插件配置
        template:'./public/index.html'//    webpack使用插件时,用来做模板的html的位置,生成html文件
    })],
    module: { //    加载器配置
        rules: [ // 规则
            { //    一个具体的规则对象
                test: /\.css$/i, // 匹配.css结尾的文件
                use: ["style-loader", "css-loader"], // webpack使用两个loader处理css文件,
                //  use数组从右到左执行的，所以顺序不能颠倒
                //  css-loader:webpack解析css文件，把css代码一起打包进js文件中
                //  style-loader:css代码插入到DOM上(style标签)
            },
        ],
    },
};
```

5.打包

执行yarn build命令

css文件整合到出口文件中

# webpack打包less文件

webpack 将 Less 编译为 CSS 的 loader。结合css-loader style-loader一块使用可将less文件一块打包

1.下载less-loader、css-loader和style-loader

```bash
yarn add webpack webpack-cli -D
yarn add css-loader style-loader -D
yarn add less-loader -D
```

2.配置package.json

```bash
"scripts":{
    "build":"webpack"
}
```

3.入口中导入css文件

```js
//  引入less文件
import './less/index.less'
```

4.package.config.js添加配置

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js',
    },
    plugins: [new HtmlWebpackPlugin({  //   plugins插件配置
        template:'./public/index.html'//    webpack使用插件时,用来做模板的html的位置,生成html文件
    })],
    module: { //    加载器配置
        rules: [ // 规则
            { //    一个具体的规则对象
                test: /\.css$/i, // 匹配.css结尾的文件
                use: ["style-loader", "css-loader"], // webpack使用两个loader处理css文件,
                //  use数组从右到左执行的，所以顺序不能颠倒
                //  css-loader:webpack解析css文件，把css代码一起打包进js文件中
                //  style-loader:css代码插入到DOM上(style标签)
            },
            {
                test: /\.less$/i, //    匹配.less结尾的文件
                use: [
                    // less-style:compiles Less to CSS
                    'style-loader',
                    'css-loader',
                    'less-loader',
                ],
            },
        ],
    },
};
```

5.打包

执行yarn build命令

less文件整合到出口文件中

# webpack处理图片

1.根据具体需求下载webpack、webpack-cli、less-loader、css-loader和style-loader

```bash
yarn add webpack webpack-cli -D
yarn add css-loader style-loader -D
yarn add less-loader -D
```

2.配置package.json

```bash
"scripts":{
    "build":"webpack"
}
```

3.设置css

```css
body{
  background: url("../assets/logo_small.png") no-repeat center;
}
```

4.入口中引入css文件，图片文件

```js
//	/src/main.js--入口

//  1.yarn add jquery
//  2.public/index.html -li*10
//  3.入口处引入jquery
import $ from "jquery"

//  引入css文件
import './css/index.css'

//  引入图片文件
//  webpack所有资源都看作模块
import imgObj from './assets/1.gif'
let theImg=document.createElement('img')
theImg.src=imgObj
document.body.appendChild(theImg)
```

5.package.config.js添加配置

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js',
    },
    plugins: [new HtmlWebpackPlugin({  //   plugins插件配置
        template:'./public/index.html'//    webpack使用插件时,用来做模板的html的位置,生成html文件
    })],
    module: { //    加载器配置
        rules: [ // 规则
            { //    一个具体的规则对象
                test: /\.css$/i, // 匹配.css结尾的文件
                use: ["style-loader", "css-loader"], // webpack使用两个loader处理css文件,
                //  从右到左的，所以顺序不能颠倒
                //  css-loader:webpack解析css文件，把css代码一起打包进js文件中
                //  style-loader:css代码插入到DOM上(style标签)
            },
            {
                test: /\.less$/i, //    匹配.less结尾的文件
                use: [
                    // compiles Less to CSS
                    'style-loader',
                    'css-loader',
                    'less-loader',
                ],
            },
            {
                test: /\.(gif|png|jpg|jpeg)/,
                type:'asset',//  匹配上面的文件后，webpack会把他们当中静态资源处理打包
                //  asset模式：
                //  以8kb大小区分文件
                //  小于8kb的，把图片转base64，打包进js中
                //  大于8kb,直接把图片输出到dist下
            }
        ],
    },
};
```

6.打包

执行yarn build命令

图片文件根据选择的模式,输出到dist目录下，或图片转base64，打包进出口js文件中

# webpack处理字体图标

字体图标属于静态资源,处理同图片

1.准备字体图标

下载字体图标，fonts文件保存到项目中

2.根据具体需求下载webpack、webpack-cli、less-loader、css-loader和style-loader

```bash
yarn add webpack webpack-cli -D
yarn add css-loader style-loader -D
yarn add less-loader -D
```

3.配置package.json

```bash
"scripts":{
    "build":"webpack"
}
```

4.入口中引入字体图标,插入网页

```js
//	/src/main.js--入口

//  1.yarn add jquery
//  2.public/index.html -li*10
//  3.入口处引入jquery
import $ from "jquery"

//  引入字体图标文件
import './assets/fonts/iconfont.css'
let theI=document.createElement("i")
theI.className="iconfont icon-qq"
document.body.appendChild(theI)
```

5.package.config.js添加配置

```javascript
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js',
    },
    plugins: [new HtmlWebpackPlugin({  //   plugins插件配置
        template:'./public/index.html'//    webpack使用插件时,用来做模板的html的位置,生成html文件
    })],
    module: { //    加载器配置
        rules: [ // 规则
            { //    一个具体的规则对象
                test: /\.css$/i, // 匹配.css结尾的文件
                use: ["style-loader", "css-loader"], // webpack使用两个loader处理css文件,
                //  从右到左的，所以顺序不能颠倒
                //  css-loader:webpack解析css文件，把css代码一起打包进js文件中
                //  style-loader:css代码插入到DOM上(style标签)
            },
            {
                test: /\.less$/i, //    匹配.less结尾的文件
                use: [
                    // compiles Less to CSS
                    'style-loader',
                    'css-loader',
                    'less-loader',
                ],
            },
            {
                test: /\.(gif|png|jpg|jpeg)$/,
                type:'asset',//  匹配上面的文件后，webpack会把他们当中静态资源处理打包
                //  asset模式：
                //  以8kb大小区分文件
                //  小于8kb的，把图片转base64，打包进js中
                //  大于8kb,直接把图片输出到dist下
            },
            {
                test: /\.(ttf|svg|eot|woff|woff2)$/,
                type: 'asset/resource',//   所有的字体图标文件，都输出到dist目录下
                generator:{ //  生成文件名字,定义规则
                    filename:'fonts/[name].[hash:6][ext]',
                    //  fonts：目录
                    //  [name]:原来的名字
                    //  [hash:6]:6位哈希值
                    //  [ext]:拓展名,[ext]会替换成.eot/.woff
                },
            }
        ],
    },
};
```

6.打包

执行webpack build命令

字体图标文件根据选择的资源模式，自定义文件名，输出到dist目录下

# webpack降级高版本js

babel是一个编译器，可将js代码输出成浏览器兼容的代码，既对高版本js语法降级处理

babel-loader:允许你使用 [Babel](https://github.com/babel/babel) 和 [webpack](https://github.com/webpack/webpack) 转译 `JavaScript` 文件

1.安装包

```ba
yarn add webpack webpack-cli -D
yarn add babel-loader @babel/core @babel/preset-env -D
```

2.配置package.json

```bash
"scripts":{
    "build":"webpack"
}
```

3.配置package.config.js

```js
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
    entry: './src/main.js',
    output: {
        path: path.resolve(__dirname, './dist'),
        filename: 'bundle.js',
    },
    plugins: [new HtmlWebpackPlugin({  //   plugins插件配置
        template:'./public/index.html'//    webpack使用插件时,用来做模板的html的位置,生成html文件
    })],
    module: { //    加载器配置
        rules: [ // 规则
            { //    一个具体的规则对象
                test: /\.css$/i, // 匹配.css结尾的文件
                use: ["style-loader", "css-loader"], // webpack使用两个loader处理css文件,
                //  从右到左的，所以顺序不能颠倒
                //  css-loader:webpack解析css文件，把css代码一起打包进js文件中
                //  style-loader:css代码插入到DOM上(style标签)
            },
            {
                test: /\.m?js$/,//  匹配.mjs  .js结尾的文件
                exclude: /(node_modules|bower_components)/,//   不去匹配这些文件夹下的文件
                use: {
                    loader: 'babel-loader',//   使用这个loader处理js文件
                    options: {
                        //  预设:@babel/preset-env降级规则,按照这里的降级js语法
                        presets: ['@babel/preset-env']
                    }
                }
            }
        ],
    },
};
```

4.打包

# webpack开发服务器

1.下载模块包

```bash
yarn add webpack-dev-server -D
```

2.配置package.json

```json
"scripts":{
    "build":"webpack",
    "server":"webpack server"
}
```

server:启动服务器命令，使用yarn serve即可启动服务器

3.更改端口

```js
module.exports={
    //	...其他配置
    devServer:{
        port:6900 //	端口号
    }
}
```

4.启动服务器

yarn server

项目文件修改时，服务器自动检测，更新修改信息