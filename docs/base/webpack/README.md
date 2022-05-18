# WebPack

## 初使化项目
* 创建一个文件夹，并初始化
```cmd
    npm init -y
```

## 安装webpack
```
    npm i webpack webpack-cli -D
```


## 运行webpack
* 在`package.json`的`scripts`中新增`"build": "webpack"`
```cmd
    npm run build
```
* 会提示错误，需要新建`src`目录，并新建`index.js`文件
* 再次运行，即可自动生成`dist`目录与`main.js`文件


## 自定义配置
* 在根目录新建`webpack.config.js`文件，参考[webpack配置](https://webpack.docschina.org/configuration/)
```js
// webpack.config.js
// ===单入口===
const path = require('path')

module.exports = {
    // 打包模式
    mode: 'production', // development production
    // 单入口
    entry: path.join(__dirname, 'src/main.js'),
     // 出口
    output: {
        path: path.join(__dirname, 'dist'),
        filename: "borders.js"
    }
}

// ===多入口===
module.exports = {
    mode: 'production',
    // 多入口
    entry: {
        main1: path.join(__dirname, 'src/main.js'),
        main2: path.join(__dirname, 'src/main2.js')
    },
    // 出口
    output: {
        path: path.join(__dirname, 'dist'),
        filename: "[name][chunkhash:6].js"// bundle.[chunkhash:8].js
    }
}
```


## 使用html-webpack-plugin 定义网页模板文件
* 安装插件
```cmd
    npm i  html-webpack-plugin -D
```

* 添加`plugin`代码
```js
// webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin');
 plugins: [
        new HtmlWebpackPlugin({
            title: '学习webpack真好玩',
            // 可以在 public/index.html通过 <%= htmlWebpackPlugin.options.title %>定义网页的标题
            template: path.join(__dirname, 'public/index.html')
        })
    ]
```

* 根目录新建`public.index.html`文件
```
将title的内容换成
<%= htmlWebpackPlugin.options.title %>
```
* 重新执行打包，查看效果
```cmd
  npm run build
```

* 安装自动清理插件
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

// 再添加
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        // 注意: 有多个loader时 loader执行过程 从后向前
        use: [
          'style-loader',
          'css-loader'
        ]
      }
    ]
  }
}

// 第二种写法 自定义loader一些配置
module.exports = {
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          {
            loader: 'style-loader',
            // 自定义配置
            options: {
               insert: 'body'
            }
          },
          {
            loader: 'css-loader',
            options: {
             
            }
          }
        ]
      }
    ]
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
            test: /\.scss$/,  // 以scss结尾
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
  npm install -D babel-loader @babel/core @babel/preset-env
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
      "serve": "webpack-dev-server"  // 新增
    }
```



