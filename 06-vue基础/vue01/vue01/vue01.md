# Vue第一天 - webpack （了解即可）

# 一. 自学部分

## 1.1 yarn包管理器

快速、可靠、安全的依赖管理工具。和 npm 类似, 都是包管理工具, 可以用于下载包, 解决国内使用npm可能出现无法访问的状况。

中文官网地址: https://yarn.bootcss.com/

### 1.1.1 下载yarn

下载地址:  https://yarn.bootcss.com/docs/install/#windows-stable 

* windows - 软件包(在笔记文件夹里)

* mac - 通过homebrew安装(看上面地址里)

  * mac如果没安装过homeBrew先运行这个命令

    ```bash
    /usr/bin/ruby -e "$(curl -fsSL http://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install)"
    ```

* 上面命令不行: 试试这个: curl -o- -L https://yarnpkg.com/install.sh | bash (直接安装yarn)

*注: 不要安到带中文的路径下, 建议在C盘*

### 1.1.2 使用yarn

与npm类似, 可以试试, 新建一个空白文件夹, 执行以下命令尝试一下

```bash
# 1. 初始化, 得到package.json文件(终端路径所在文件夹下)
yarn init
```

![image-20220531174756796](images/image-20220531174756796.png)

```bash
# 2. 添加依赖(下包)
# 命令: yarn add [package]
# 命令: yarn add [package]@[version]
yarn add jquery
yarn add jquery@3.5.1

# 如果yarn没办法下载依赖包那么可以尝试使用cnpm
# 命令: cnpm i [package]
# 命令: cnpm i [package]@[version]
cnpm i jquery
cnpm i jquery@3.5.1
```

![image-20220531175811640](images/image-20220531175811640.png)

![image-20220531175936373](images/image-20220531175936373.png)

```bash
# 3. 移除包
# 命令: yarn remove [package]
yarn remove jquery
```

![image-20220531180233227](images/image-20220531180233227.png)

```bash
# 4. 安装项目全部依赖(一般拿到别人的项目时, 缺少node_modules)          
yarn
# 会根据当前项目package.json记录的包名和版本, 全部下载到当前工程中

# 5. 全局
# 安装: yarn global add [package]
# 卸载: yarn global remove [package]
# 注意: global一定在add左边
yarn global add @vue/cli
# 如何使用, 为明天学习vue做铺垫
```

### 1.1.3 cnpm （中国镜像站）

> 如何快速的安装cnpm https://blog.csdn.net/qq_25972233/article/details/122850862



## 1.2 知识点自测

对这些知识点了如指掌, 学习今天的内容会轻松很多

- [ ] 什么是模块, 模块化开发规范(CommonJS / ES6)

  commonJS规范:

  ```js
  // nodejs - commonJS规范-规定了导出和导入方式
  // 导出 module.exports = {}
  // 导入 const 变量 = require("模块标识")
  ```

  ES6规范

  ```js
  // 导出 export 或者 export default {}
  // 导入 import 变量名 from '模块标识'
  ```

- [ ] 字体图标的使用

  1. 可以去阿里巴巴矢量图标库, 选中想要的图标, 登录后, 生成css文件和字体文件
  2. 下载css文件和字体文件, 也可以使用在线地址
  3. 在自己页面中引入iconfont.css, 并在想显示字体图标的标签上使用类名即可

- [ ] 箭头函数非常熟练

  ```js
  const fn = () => {}   
  fn()
  
  const fn2 = (a, b) => {return a + b} 
  fn(10, 20); // 结果是30
  
  // 当形参只有一个()可以省略
  const fn3 = a => {return a * 2}
  fn(50); // 结果是100
  
  // 当{}省略return也省略, 默认返回箭头后表达式结果
  const fn4 = a => a * 2;
  fn(50); // 结果是100
  ```

- [ ] 什么是服务器, 本地启动node服务, 服务器和浏览器关系, 服务器作用

  ```bash
  #服务器是一台性能高, 24小时可以开机的电脑
  
  #服务器可以提供服务(例如: 文件存储, 网页浏览, 资源返回)
  
  #在window电脑里安装node后, 可以编写代码用node 启动一个web服务, 来读取本地html文件, 返回给浏览器查看
  
  #浏览器 -> 请求资源 -> 服务器
  
  #浏览器 <-  响应数据 <- 服务器
  ```

- [ ] 开发环境 和 生产环境 以及英文"development", "production" 2个单词尽量会写会读

- [ ] 初始化包环境和package.json文件作用

  ```bash
  npm下载的包和对应版本号, 都会记录到下载包时终端所在文件夹下的package.json文件里
  ```

- [ ] package.json中的dependencies和 devDependencies区别和作用

  ```bash
  * dependencies  别人使用你的包必须下载的依赖, 比如yarn add  jquery
  
  * devDependencies 开发你的包需要依赖的包,  比如yarn add webpack  webpack-cli -D (-D 相当于 --save-dev)
  ```

- [ ] 终端的熟练使用: 切换路径, 清屏, 包下载命令等

  ```bash
  切换路径  cd  
  
  清屏 cls 或者 clear
  ```

- [ ] 对base64字符串, 图片转base64字符串了解

  在线装换图片http://tool.chinaz.com/tools/imgtobase/

  

# 今日学习目标（会查就行）

1. 能够理解webpack基本概念和作用

2. 能够掌握webpack使用步骤

3. 能够使用webpack相关配置

4. 能够使用webpack开发服务器

5. 能够查阅使用webpack中文文档

# 一. webpack基本概念

## 1.1 本质

webpack是node的一个第三方模块包, 用于打包代码

[webpack官网](https://webpack.docschina.org/)

* 现代 javascript 应用程序的 **静态模块打包器 (module bundler)**

* 为要学的 vue-cli 开发环境做铺垫

## 1.2 作用

把很多文件打包整合到一起, 缩小项目体积, 提高加载速度

![image-20220531192547432](images/image-20220531192547432.png)

其中功能:

* less/sass -> css

* ES6/7/8 -> ES5（兼容）

* html/css/js -> 压缩合并

# 二. webpack使用步骤

## 2.1 webpack基础使用

> 目标： 将两个`src`文件夹中的两个`js`温江打包到一个`js`中，并输出到默认的`dist`目录（文件夹）下

### 2.1.1 准备工作

1. 初始化包环境（创建`package.json`）

   > `package.json`是一个项目描述文件, 里面记录了当前项目的信息。eg: 项目名称、版本、作者、[gitHub](https://so.csdn.net/so/search?q=gitHub&spm=1001.2101.3001.7020)地址、当前项目依赖哪些第三方模块等。 使用`npm`安装第三方模块，是模块的相关信息会自动添加到`package.json`文件中。它在项目中扮演着记录员的角色

   ```
   npm init
   ```

   

2. 安装依赖包

   ```bash
   npm i webpack webpack-cli -D
   ```

   `-D`：表示将`webpack、webpack-cli`这两个包记录在开发环境

   ![image-20220531194013766](images/image-20220531194013766.png)

3. 配置scripts(自定义命令)

   ```bash
   "scripts": {
   	"build": "webpack"
   }
   ```

   ![image-20220531194111785](images/image-20220531194111785.png)

### 2.1.2 将两个JS文件打包成一个文件

> ##### 在插件库中找到美化文件UI的工具[Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme)

> 必须放到src文件夹下，webpack会默认去src文件夹下找文件打包

4. 新建目录src

5. 新建`src/add/add.js` - 定义一个求和函数并导出

   ```js
   export const addFn = (a, b) => a + b
   ```

6. 新建`src/index.js`导入add.js并使用

   > 这个`src/index.js`文件是默认的webpack打包入口，一定要这么写

   ```js
   // webpack打包的入口
   // 按需导入使用{}
   import {addFn} from './add/add'
   
   console.log(addFn(10, 20));
   ```

   ![image-20220531194901232](images/image-20220531194901232.png)

7. 运行打包命令

   ```bash
   npm run build
   #或者 yarn build
   #或者 cnpm run build
   ```

   ![image-20220531195032137](images/image-20220531195032137.png)

**总结：**src的兄弟文件夹, 生成默认dist目录和打包后默认main.js文件

![image-20220531195127509](images/image-20220531195127509.png)

问： 如何使用webpack并进行打包操作？



## 2.2 webpack 更新打包

> 目标: 以后代码变更, 如何重新打包呢

1. 新建`src/tool/tool.js` - 定义导出数组求和方法

   > 模拟新建业务代码，当项目功能扩展时自然会新增新的代码文件

   ```js
   export const getArrSum = arr => arr.reduce((sum, val) => sum += val, 0)
   ```

2. `src/index.js` - 导入使用

   ```js
   // webpack打包的入口
   // 按需导入使用{}
   import {addFn} from './add/add'
   import {getArrSum} from './tool/tool'
   
   console.log(addFn(10, 20));
   console.log(getArrSum([1, 2, 3]));
   ```

3. 重新打包

   ```bash
   npm run build
   #或者 yarn build
   #或者 cnpm run build
   ```

   ![image-20220531200340657](images/image-20220531200340657.png)

> 总结：
>
> 1. src中是开发环境， 与dist打包后的文件湘湖独立
> 2. 打包后格式压缩，变量压缩（体积更小）



# 三. webpack的配置

## 3.1 `webpack`-入口和出口

> webpack打包文件时的默认文件夹是？
>
> 默认的js入口文件是？
>
> 默认的打包后的js出口文件是？

1. 读webpack文档

   > https://webpack.docschina.org/concepts/#entry

   ![image-20220531203017418](images/image-20220531203017418.png)

2. webpack配置 - webpack.config.js(默认)

3. 新建`webpack.config.js`

   >  与package.json同级

   ![image-20220531203418748](images/image-20220531203418748.png)

4. 填入配置项

   1. 将默认入口`index.js`改成`main.js`
   2. 填入配置

   ```js
   // path 模块提供了一些实用工具，用于处理文件和目录的路径。
   const path = require("path")
   
   module.exports = {
       entry: "./src/main.js", // 入口 注意是相对路径
       output: { // 出口
        	// __dirname 表示当前文件：webpack.config.js 的当前文件的目录名
           path: path.join(__dirname, "dist"), // 出口路径 文件夹名称
           filename: "bundle.js" // 出口js文件名
       }
   }
   ```

5. 打包

   ```bash
   yarn build
   ```

![image-20220531204609333](images/image-20220531204609333.png)

问： 如何修改`webpack`的入口和出口？

## 3.2 打包流程图

> yarn build 打包时，经历了那些过程？

![image-20220531204909616](images/image-20220531204909616.png)

**重点: 所有要被打包的资源都要跟入口产生直接/间接的引用关系**

## 3.3 案例-webpack隔行变色

> 需求： 通过jquery，模块化引入到js中，编写代码实现变色
>
> ![image-20220601095251652](images/image-20220601095251652.png)

**步骤：**

1. 从零开始搭建环境

   1. 初始化包环境
   2. 下载依赖包
   3. 配置自定义打包命令

2. 下载jquery， 新建`public/index.html`

   ```
   npm i jquery
   ```

   ![image-20220601095633593](images/image-20220601095633593.png)

3. 给index.html添加一些`li`标签

   ```html
   <body>
     <div id="app">
       <!-- ul>li{我是第$个li}*10 -->
       <ul>
         <li>我是第1个li</li>
         <li>我是第2个li</li>
         <li>我是第3个li</li>
         <li>我是第4个li</li>
         <li>我是第5个li</li>
         <li>我是第6个li</li>
         <li>我是第7个li</li>
         <li>我是第8个li</li>
         <li>我是第9个li</li>
       </ul>
     </div>
   </body>
   ```

4. 在`src/main.js`引入`jquery`,`src/main.js`中编写隔行变色代码

   ```js
   // 引入jquery
   import $ from 'jquery'
   $(function() {
     $('#app li:nth-child(odd)').css('color', 'red') // 奇数红色
     $('#app li:nth-child(even)').css('color', 'green') // 偶数绿色
   })
   ```

5. 执行打包命令观察效果

   ![image-20220601100131998](images/image-20220601100131998.png)

6. 在dist下把public/index.html拷贝过来，手动引入js

   ![image-20220601100235293](images/image-20220601100235293.png)

   ```vue
   <script src="./bundle.js"></script>
   ```

   ![image-20220601100307009](images/image-20220601100307009.png)

   > 总结: 前端工程化模块化, 需要的包通过yarn下载，被webpack打包后引入到html中使用

**思考：**每次打包结束后都需要手动去引入html文件并且手动导入js文件真的合理吗？



## 3.4 插件-自动生成html文件

> 目标: html-webpack-plugin插件, 让webpack打包后生成html文件并自动引入打包后的js
>
> [html-webpack-plugin插件地址](https://www.webpackjs.com/plugins/html-webpack-plugin/)

![image-20220601100537823](images/image-20220601100537823.png)

  1. 下载插件

     ```dash
     yarn add html-webpack-plugin -D
     ```

     ![image-20220601102350619](images/image-20220601102350619.png)

  2. webpack.config.js配置

     ```js
     // path 模块提供了一些实用工具，用于处理文件和目录的路径。
     const path = require("path")
     const HtmlWebpackPlugin = require('html-webpack-plugin')
     
     module.exports = {
         entry: "./src/main.js", // 入口 注意是相对路径
         output: { // 出口
             // __dirname 表示当前文件：webpack.config.js 的当前文件的目录名
             path: path.join(__dirname, "dist"), // 出口路径 文件夹名称
             filename: "bundle.js" // 出口js文件名
         },
         plugins: [ // plugins插件配置
             new HtmlWebpackPlugin({
                 template: './public/index.html' // 告诉webpack使用插件时, 以我们自己的html文件作为模板去生成dist/html文件
             })
         ]
     }
     ```

  3. 重新打包后观察dist下是否多出html并运行看效果

     ![image-20220601103619762](images/image-20220601103619762.png)

> 总结:  webpack.config.js就是一个配置表，需要的功能就在config中配置

## 3.5 加载器 - 处理css文件问题(测试是否可以打包css)

> 目标: 自己准备css文件, 引入到webpack入口, 测试webpack是否能打包css文件
>
> 得到结果： webpack**默认**只能处理js类型文件

1. 新建 - src/css/index.css

   ![image-20220601104547006](images/image-20220601104547006.png)

2. 编写去除li圆点样式代码

   ```css
   li{
       list-style: none;
   }
   ```

3. (重要) 一定要引入到入口才会被webpack打包

   ```js
   // 引入css文件
   import "./css/index.css" 
   ```

   ![image-20220601104811251](images/image-20220601104811251.png)

4. 执行打包命令观察效果

   报错了！！

   ![image-20220601104901786](images/image-20220601104901786.png)

> 总结: 保存原因, 因为webpack**默认**只能处理js类型文件



## 3.6 加载器 - 处理css文件

> 原因: webpack默认只认识 js 文件和 json文件
>
> 目标: loaders加载器, 可让webpack处理**其他类型**的文件, 打包到js中
>
> [style-loader文档](https://webpack.docschina.org/loaders/style-loader/)：把css插入到dom中
>
> [css-loader文档](https://webpack.docschina.org/loaders/css-loader/)：`css-loader` 会对 `@import` 和 `url()` 进行处理，就像 js 解析 `import/require()` 一样

1. 安装依赖

   ```dash
   npm i style-loader css-loader -D
   ```

2. webpack.config.js 配置

   ```js
   module.exports = {
   	// ... 未修改代码省略
       module: { // 加载器配置
           rules: [ // 规则
               { // 一个具体的规则对象
                   test: /\.css$/i, // 匹配.css结尾的文件
                   use: ["style-loader", "css-loader"], // 让webpack使用这2个loader处理css文件
                   // 执行顺序是从右到左的, 所以不能颠倒顺序
                   // css-loader: webpack解析css文件-把css代码一起打包进js中
                   // style-loader: css代码插入到DOM上 (style标签)
               },
           ],
       },
   }
   ```

3. 运行打包后dist/index.html观察效果和css引入情况

   ![image-20220601105752023](images/image-20220601105752023.png)

> 总结: 万物皆模块, 引到入口, 才会被webpack打包， 如：css打包进js中, 然后被嵌入在style标签插入dom上

## 3.7 加载器 - 处理less文件

> 目标: less-loader让webpack处理less文件, less模块翻译less代码

[less-loader文档](https://webpack.docschina.org/loaders/less-loader/)： webpack 将 Less 编译为 CSS 的 loader。

1. 下载依赖包

   ```bash
   npm i less less-loader -D
   ```

   ![image-20220601110407784](images/image-20220601110407784.png)

2. webpack.config.js 配置

   ```js
   module.exports = {
       // ...省略其他
       module: { // 加载器配置
           rules: [ // 规则
               {
                   test: /\.css$/i,
                   use: ["style-loader", "css-loader"]
               },
               {
                   test: /\.less/,
                   use: ['style-loader', 'css-loader', 'less-loader']
               }
           ]
       }
   }
   ```

3. src/less/index.less  - 设置li字体大小30px

   ```less
   @size: 30px;
   li{
       font-size: @size;
   }
   ```

   ![image-20220601110757066](images/image-20220601110757066.png)

4. 引入到main.js中

   ```js
   import "./less/index.less"
   ```

5. 打包运行dist/index.html 观察效果

   ![image-20220601110928391](images/image-20220601110928391.png)

> 总结: 只要找到对应的loader加载器, 就能让webpack处理不同类型文件

## 3.8 加载器 - 处理图片文件

> 目标: 用asset module方式(webpack5版本新增)

[asset module文档](https://webpack.docschina.org/guides/asset-modules/)：资源模块(asset module)是一种模块类型，它允许使用资源文件（字体，图标等）而无需配置额外 loader。

*注： 如果使用的是webpack5版本的（现在一般也是用的webpack5）, 直接配置在webpack.config.js - 的 rules里即可*

```js
{
    test: /\.(png|jpg|gif|jpeg)$/i,
    type: 'asset'
}
```

如果你用的是webpack4及以前的, 请使用者里的配置

[url-loader文档](https://webpack.docschina.org/loaders/url-loader/)：它把文件转换成base64 uri

[file-loader文档](https://webpack.docschina.org/loaders/file-loader/)：将文件上的import/require()解析为一个url，并将该文件发送到输出目录。

1. 下载依赖包

   ```dash
   npm i url-loader file-loader -D
   ```

2. webpack.config.js 配置

   ```js
   module.exports = {
       // ...省略其他
       module: { // 加载器配置
           rules: [ // 规则
               {
                   test: /\.css$/i,
                   use: ["style-loader", "css-loader"]
               },
               {
                   test: /\.less/,
                   use: ['style-loader', 'css-loader', 'less-loader']
               },
               { // 图片文件的配置(仅适用于webpack5版本)
                   test: /\.(gif|png|jpg|jpeg)/,
                   type: 'asset' // 匹配上面的文件后, webpack会把他们当做静态资源处理打包
                   // 如果你设置的是asset模式
                   // 以8KB大小区分图片文件
                   // 小于8KB的, 把图片文件转base64, 打包进js中
                   // 大于8KB的, 直接把图片文件输出到dist下
               }
           ]
       }
   }
   ```

   图片转成 base64 字符串

   - 好处就是浏览器不用发请求了，直接可以读取
   - 坏处就是如果图片太大，再转`base64`就会让图片的体积增大 30% 左右

3. 准备工作

   1. src/assets/中放入预设好的图片文件

      ![image-20220601112131449](images/image-20220601112131449.png)

   2. 在css/less/index.less - 把小图片用做背景图

      ```less
      body{
          background: url(../assets/logo_small.png) no-repeat center;
      }
      ```

   3. 在src/main.js - 把大图插入到创建的img标签上, 添加body上显示

      ```js
      // 引入图片-使用
      // webpack眼里万物皆模块
      import imgUrl from './assets/1.gif'
      const theImg = document.createElement("img")
      theImg.src = imgUrl
      document.body.appendChild(theImg)
      ```

   4. 打包运行dist/index.html查看2个图片的区别

      ![image-20220601112920161](images/image-20220601112920161.png)

   > 思考：为什么一个打包出来是base64格式，而另一个就是图片路径

## 3.9 webpack加载文件优缺点

图片转成 base64 字符串

- 好处就是浏览器不用发请求了，直接可以读取
- 坏处就是如果图片太大，再转`base64`就会让图片的体积增大 30% 左右

## 3.10 加载器 - 处理字体文件

> 目标: 用asset module技术, asset/resource直接输出到dist目录下
>
> [资源模块resource](https://webpack.docschina.org/guides/asset-modules/#resource-assets)资源模块(asset module)是一种模块类型，它允许使用资源文件（字体，图标等）而无需配置额外 loader。

1. webpack.config.js - 准备配置

   webpack5使用这个配置

```js
{ // webpack5默认内部不认识这些文件, 所以当做静态资源直接输出即可
              test: /\.(eot|svg|ttf|woff|woff2)$/,
                type: 'asset/resource', // 所有的字体图标文件, 都输出到dist下
                generator: { // 生成文件名字 - 定义规则
                    filename: 'fonts/[name].[hash:6][ext]' // [ext]会替换成.eot/.woff
                }
}
```

webpack4及以前使用下面的配置

```js
{ // 处理字体图标的解析
    test: /\.(eot|svg|ttf|woff|woff2)$/,
        use: [
            {
                loader: 'url-loader',
                options: {
                    limit: 2 * 1024,
                    // 配置输出的文件名
                    name: '[name].[ext]',
                    // 配置输出的文件目录
                    outputPath: "fonts/"
                }
            }
        ]
}
```

1. src/assets/ - 放入字体库fonts文件夹

   ![image-20220601113641625](images/image-20220601113641625.png)

2. 在main.js引入iconfont.css

   ```js
   // 8. 引入字体图标样式文件
   import "./assets/fonts/iconfont.css"
   let theI = document.createElement("i")
   theI.className = "iconfont icon-qq"
   document.body.appendChild(theI)
   ```

3. 执行打包命令 - 观察打包后网页效果

   ![image-20220601114832269](images/image-20220601114832269.png)

> 总结: url-loader和file-loader 可以打包静态资源文件

## 3.11 加载器 - 处理高版本js语法(面试小点)

> 场景：高版本的js代码(箭头函数), 打包后, 直接原封不动打入了js文件中, 遇到一些低版本的浏览器就会报错
>
> 目标: 让webpack对高版本 的js代码, 降级处理后打包
>
> 原因: **webpack 默认仅内置了 模块化的 兼容性处理**   `import  export`
>
> babel 的介绍 => 用于处理高版本 js语法 的兼容性  [babel官网](https://www.babeljs.cn/)
>
> [babel-loader文档](https://webpack.docschina.org/loaders/babel-loader/)：允许你使用 [Babel](https://github.com/babel/babel) 和 [webpack](https://github.com/webpack/webpack) 转译 `JavaScript` 文件。
>
> 解决: 让webpack配合babel-loader 对js语法做处理

1. 安装包

   ```bash
   npm i -D babel-loader @babel/core @babel/preset-env
   ```

2. 配置规则

   ```js
   {
       test: /\.m?js$/,
           exclude: /(node_modules|bower_components)/, // 不去匹配这些文件夹下的文件（防止影响其他第三方依赖包）
               use: {
                   loader: 'babel-loader', // 使用这个loader处理js文件
                       options: { // 加载器选项
                           presets: ['@babel/preset-env'] // 预设: @babel/preset-env 降级规则-按照这里的规则降级我们的js语法
                       }
               }
   }
   ```

3. 如：在main.js中使用箭头函数(高版本js)

   ```js
   // 9. 书写高版本的js语法
   const fn = () => {
     console.log("我是一个箭头函数")
   }
   console.log(fn)
   ```

4. 打包后观察dist/bundle.js - 被转成成普通函数使用了 - 这就是babel降级翻译的功能

   ![image-20220601120044282](images/image-20220601120044282.png)



# 四. webpack开发服务器(热更新)

抛出问题: 每次修改代码, 都需要重新 yarn build 打包, 才能看到最新的效果, 实际工作中, 打包 yarn build 非常费时 (30s - 60s) 之间

为什么费时? 

1. 从0构建依赖
2. 磁盘读取对应的文件到内存, 才能加载  
3. 用对应的 loader 进行处理  
4. 将处理完的内容, 输出到磁盘指定目录  

> 解决问题: 起一个开发服务器,  在电脑内存中打包，缓存一些已经打包过的内容，只重新打包修改的文件，最终运行加载在内存中给浏览器使用
>
> 优势：
>
> 1. 打包在内存中，速度快
> 2. 自动更新打包变化的代码，实时返回给浏览器显示

## 4.1 webpack-dev-server自动刷新(dev环境 - 今后使用会像呼吸一样的自然)

> 目标: 启动本地服务, 可实时更新修改的代码, 打包**变化代码**到内存中, 然后直接提供端口和网页访问
>
> 文档地址: https://webpack.docschina.org/configuration/dev-server/

1. 下载模块

   ```bash
   npm i webpack-dev-server -D
   ```

2. 配置自定义命令

   ```bash
   scripts: {
   	"build": "webpack",
   	"serve": "webpack serve"
   }
   ```

3. 运行命令-启动webpack开发服务器

   ```bash
   npm run serve
   # 或者 yarn serve
   ```

   **如果报错，则需要安装`webpack-cli`**

   ```bash
   npm i --save-dev webpack-cli 
   ```

   如果npm下载依赖包超时，则可以通过设置淘宝镜像

   ```bash
   npm install -g cnpm --registry=https://registry.npm.taobao.org
   npm config set registry https://registry.npm.taobao.org
   
   # 这样npm命令就可以使用cnpm命令来代替
   ```

   启动发现回提示一个错误

   ![image-20220601135026651](images/image-20220601135026651.png)

   这里是因为wepack对语法要求更为杨哥，需要在设置中设置对应的环境模式

   ```js
     "scripts": {
       "build": "webpack --mode production", // 生产环境
       "serve": "webpack serve --mode development" // 开发环境
     },
   ```

   ![image-20220601141057716](images/image-20220601141057716.png)

4. 尝试修改代码，保存后查看页面是否修改

> 总结： 通过`webpack serve`后，修改src下的代码，会自动更新到内存打包，浏览器也会展示相应



## 4.2 webpack-dev-server配置（自定义端口号）

在webpack.config.js中添加服务器配置

更多配置参考这里: https://webpack.docschina.org/configuration/dev-server/#devserverafter

```js
module.exports = {
    // ...其他配置
    devServer: {
        port: 3000 // 端口号
    }
}
```



## 今日总结

- [ ] 什么是webpack, 它有什么作用
- [ ] 知道yarn的使用过程, 自定义命令, 下载删除包
- [ ] 有了webpack让模块化开发前端项目成为了可能, 底层需要node支持
- [ ] 对webpack各种配置项了解
  - [ ] 入口/出口
  - [ ] 插件
  - [ ] 加载器
  - [ ] mode模式
  - [ ] devServer
- [ ] webpack开发服务器的使用和运作过程



# 面试题（现在不要花时间在这里，等后续面试环节了在回过头来看）

## 1、什么是webpack

​	webpack是一个打包模块化javascript的工具，在webpack里一切文件皆模块，通过loader转换文件，通过plugin注入钩子，最后输出由多个模块组合成的文件，webpack专注构建模块化项目

## 2、Webpack的优点是什么？（可能会问）

1. 专注于处理模块化的项目，能做到开箱即用，一步到位
2. 通过plugin扩展，完整好用又不失灵活
3. 通过loaders扩展, 可以让webpack把所有类型的文件都解析打包
4. 区庞大活跃，经常引入紧跟时代发展的新特性，能为大多数场景找到已有的开源扩展

## 3、webpack的构建流程是什么?从读取配置到输出文件这个过程尽量说全（如果问到答了加分，不会说也不扣分）

​    Webpack 的运行流程是一个串行的过程，从启动到结束会依次执行以下流程：

​	1. 初始化参数：从配置文件读取与合并参数，得出最终的参数

   	2. 开始编译：用上一步得到的参数初始化 Compiler （汇编）对象，加载所有配置的插件，开始执行编译
            	3. 确定入口：根据配置中的 entry 找出所有的入口文件
         	4. 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理
                	5. 完成模块编译：在经过第4步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系
               	6. 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会
                      	7. 输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。

在以上过程中，Webpack 会在特定的时间点广播出特定的事件，插件在监听到感兴趣的事件后会执行特定的逻辑，并且插件可以调用 Webpack 提供的 API 改变 Webpack 的运行结果

### 4、说一下 Webpack 的热更新原理（背吧）

​	webpack 的热更新又称热替换（Hot Module Replacement），缩写为 HMR。这个机制可以做到不用刷新浏览器而将新变更的模块替换掉旧的模块。

​    HMR的核心就是客户端从服务端拉去更新后的文件，准确的说是 chunk diff (chunk 需要更新的部分)，实际上 WDS 与浏览器之间维护了一个 Websocket，当本地资源发生变化时，WDS 会向浏览器推送更新，并带上构建时的 hash，让客户端与上一次资源进行对比。客户端对比出差异后会向 WDS 发起 Ajax 请求来获取更改内容(文件列表、hash)，这样客户端就可以再借助这些信息继续向 WDS 发起 jsonp 请求获取该chunk的增量更新。

​    后续的部分(拿到增量更新之后如何处理？哪些状态该保留？哪些又需要更新？)由 HotModulePlugin 来完成，提供了相关 API 以供开发者针对自身场景进行处理，像react-hot-loader 和 vue-loader 都是借助这些 API 实现 HMR。

### 5、有哪些常见的Loader？他们是解决什么问题的？（必会）

1、  file-loader：把文件输出到一个文件夹中，在代码中通过相对 URL 去引用输出的文件

2、  url-loader：和 file-loader 类似，但是能在文件很小的情况下以 base64 的方式把文件内容注入到代码中去

3、  source-map-loader：加载额外的 Source Map 文件，以方便断点调试

4、  image-loader：加载并且压缩图片文件

5、  babel-loader：把 ES6 转换成 ES5

6、  css-loader：加载 CSS，支持模块化、压缩、文件导入等特性

7、  style-loader：把 CSS 代码注入到 JavaScript 中，通过 DOM 操作去加载 CSS。

8、  eslint-loader：通过 ESLint 检查 JavaScript 代码

### 6、Loader和Plugin的不同？（必会）

​    **1)** **不同的作用**

​       Loader直译为"加载器"。Webpack将一切文件视为模块，但是webpack原生是只能解析js文件，如果想将其他文件也打包的话，就会用到loader。 所以Loader的作用是让webpack拥有了加载和解析非JavaScript文件的能力。

​    Plugin直译为"插件"。Plugin可以扩展webpack的功能，让webpack具有更多的灵活性。 在 Webpack 运行的生命周期中会广播出许多事件，Plugin 可以监听这些事件，在合适的时机通过 Webpack 提供的 API 改变输出结果。

**2)** **不同的用法**

​    Loader在module.rules中配置，也就是说他作为模块的解析规则而存在。 类型为数组，每一项都是一个Object，里面描述了对于什么类型的文件（test），使用什么加载(loader)和使用的参数（options）

​    Plugin在plugins中单独配置。 类型为数组，每一项是一个plugin的实例，参数都通过构造函数传入。























