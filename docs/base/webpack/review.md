## 预备与测试
* 初始化
```
  npm init -y
```

* 安装webpack
```
  npm i webpack webpack-cli -D
```

* 新增入口文件
    - 新建src/index.js
    - 运行项目
```js
  // 添加脚本
    "scripts": {
        "build": "webpack"
    }
  // 运行脚本
  npm run build
```

## 自定义配置
* 根目录新建`webpack.config.js`
```js
// 单入口
const path = require('path')

module.exports = {
    // 打包模式
    mode: 'production', // development production
    // 单入口
    entry: path.join(__dirname, 'src/index.js'),
     // 出口
    output: {
        path: path.join(__dirname, 'dist'),
        filename: "[hash:8].js"
    }
}

```

## 自定义页面模板
* 安装依赖
```
  npm i  html-webpack-plugin -D
```

* 在`webpack.config.js`中新增`plugins`
```js
  // 引入 HtmlWebpackPlugin
  const HtmlWebpackPlugin = require('html-webpack-plugin');
  // 添加插件
    plugins: [
        new HtmlWebpackPlugin({
            title: '学习webpack真好玩',
            // 可以在 public/index.html通过 <%= htmlWebpackPlugin.options.title %>定义网页的标题
            template: path.join(__dirname, 'public/index.html')
        })
    ]
```

* 根目录新建`public/index.html`文件
```
将title的内容换成
<%= htmlWebpackPlugin.options.title %>
```
* 重新执行打包，查看效果
```cmd
  npm run build
```


* 安装自动清理插件，不需要手动删除dist目录了
```js
  // 安装
  npm install clean-webpack-plugin -D
  // 引入
  const { CleanWebpackPlugin } = require('clean-webpack-plugin');
  // 在 plugin中添加该实例
  new CleanWebpackPlugin()
```

## webpack的资源解析器loader
* 在js中解析，对应的其他类型的资源，不同类型的资源需要不同的`loader`
* 比如：
    - vue `vue-loader`
    - css `css-loader`
    - ...

### 处理程序中的样式文件
* CSS文件
```js
// 先安装
  npm i css-loader -D    //  js会解析css
  npm i style-loader -D  // 将解析好的css写入style标签，并插入到头部中
// 在入口文件引入css
import './assets/index.css'
// 再添加
module.exports = {
 module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          'style-loader',
          'css-loader'
        ]
      }
    ],
  }
}
```

* CSS预处理器
    - less  less、less-loader 
    - sass  node-sass、sass-loader

```js
// 安装
cnpm i less less-loader -D
cnpm i node-sass sass-loader -D

// 使用
module.exports = {
    module: {
        rules: [
       {
        test: /\.less$/,
        use: [
          'style-loader',
          'css-loader',
          'less-loader'
        ]
      },
      {
        
        test: /\.scss$/,  // 文件以scss结尾
        use: [
          'style-loader',
          'css-loader',
          'sass-loader'
        ]
      },
        ]
    }
}
```

## ES6 的 babel
```js
  // 安装
  npm i babel-loader @babel/core @babel/preset-env -D
  // 使用 1 babel配置写在babel-loader
 module: {
    rules: [
      {
        test: /\.m?js$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: [
              ['@babel/preset-env', { targets: "defaults" }]
            ]
          }
        }
      }
    ]
  }

  // 2 配置 定义在 根目录下的babel.config.js中
  // 2-1 将babel-loader 中的 options删除
  module: {
    rules: [
      {
        test: /\.m?js$/,
        exclude: /node_modules/,
        use: ['babel-loader']
      }
    ]
  }
  // 2-2  根目录下创建babel.config.js
  module.exports = {
    presets: [
      '@babel/preset-env'
    ]
  }
```

## 处理静态资源
* webpack从5.x开始，内置了静态资源处理 [资源模块](https://webpack.docschina.org/guides/asset-modules/)
  - asset/resource 发送一个单独的文件并导出 URL。
  - asset/inline 导出一个资源的 data URI。base64格式
  - asset 在导出一个 data URI 和发送一个单独的文件之间自动选择。

```js
rules: [
     {
        test: /\.(png|jpe?g|gif)$/i,
        type: 'asset',
        parser: {
          dataUrlCondition: {
            maxSize: 200 * 1024 // 200kb 小于就转base64
          }
        }
      }
  ]
```

## 定义路径别名和 省略后缀名
js、vue的文件可以省略后缀名，参考[解析(Resolve)](https://webpack.docschina.org/configuration/resolve/)
```js
  module.exports = {
    resolve: {
      alias: {
        "@": path.join(__dirname, 'src')
      },
      extensions: ['.js', '.json', '.vue']
    }
  }
```

## 配置开发环境服务器
```js
  // 安装
  npm i webpack-dev-server -D

  // 添加
  module.exports = {
  devServer: {
    static: {
      directory: path.join(__dirname, 'public'),
    },
    // 是否开启 gzip压缩
    compress: true,
    port: 9000,
    open: true
  }
}

// 添加package.json脚本
  "scripts": {
      "build": "webpack",
      "serve": "webpack-dev-server"
    }
```

## 搭建vue spa环境
* 基础配置
```js
  // 安装vue相关依赖
  npm i vue-loader vue-template-compiler vue-style-loader -D

  // 引入 VueLoaderPlugin
  // const VueLoaderPlugin = require('vue-loader/lib/plugin');
  const { VueLoaderPlugin } = require('vue-loader')

  // 新增插件
  new VueLoaderPlugin()

  // 新增规则
  {
    test: /\.vue$/,
    use: ['vue-loader']
  }
```

* 其他准备
  + 新建`public/index.html`
    - 更改标题为`<%= htmlWebpackPlugin.options.title %>`
    - 添加 `<div id="app"></div>`
  + 新建`src/`
    - `src/assets/`
    - `src/components/`
    - `src/css/`
    - `src/router/`
    - `src/views/`
    - `src/App.vue` // 保留路由出口
        <template>
            <div id="app">
                <router-view />
            </div>
        </template>
    - `src/main.js`

* 安装依赖
```
  npm i vue vue-router -S
```


