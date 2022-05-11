<!-- 
* 该文件是子目录的路由默认页
* 默认不显示目录，可以设置开启侧边栏的目录显示，该文件的目录会显示在侧边栏
* 侧边栏默认显示的一级目录，是通过根目录的_sidebar.md文件定义的。
* 嵌套目录显示是从二级目录开始的，subMaxLevel: 5 能够显示到四级目录
* 如果未开启嵌套
-->

# HTML
> 教程参考：[MDN](https://developer.mozilla.org/zh-CN/docs/Learn/HTML)、 [菜鸟教程](https://www.runoob.com/html/html-tutorial.html)、[W3school](https://www.w3school.com.cn/html/index.asp)


## web网页组成
* 结构  `HTML`
* 表现  `CSS`
* 行为  `JavaScript`


## 文件命名规则
* 名称全部用小写英文字母、数字、下划线的组合
* 其中不得包含汉字、空格和特殊字符，必须以英文字母开头
* 最好使用语义化比较强的英文


## HTML与XHTML的区别

* `HTML` 指的是超文本标记语言 (Hyper Text Markup Language) www万维网的描述性语言。
* `XHTML` 指可扩展超文本标记语言（标识语言）（EXtensible HyperText Markup Language）是一种置标语言，表现方式与超文本标记语言（HTML）类似，不过语法上更加严格。
  - `XHTML`元素必须被正确地嵌套
  - `XHTML`元素必须被关闭
  - `XHTML`标签名必须用小写字母
  - `XHTML`文档必须拥有根元素



## HTML语法

* **双标签**，标签的`/`不能丢失
```html
  <标签 属性=“属性值”></标签>
```

* **单标签**，标签的`/`可带也可不带
```html
  <标签 属性=“属性值” >
  <标签 属性=“属性值” />
```


## HTML常用标签

### 高频标签
* **划分页面区域**
```html
  <div>内容</div>
```

* **文本节点**
```html
  <span>内容</span>
```


### 文本标题
```html
  <h1>文章或者重点标题</h1> 
  <h2>大模块的标题</h2> 
  <h3>小模块的标题</h3> 
  <h4>标题H4</h4> 
  <h5>标题H5</h5>
  <h6>标题H6</h6>
```


### 段落
```html
  <p>段落文本内容</p>
```


### 加粗
* 相同点：视觉效果一样，都可以加粗
* 不同点，`b`是单纯的加粗，`strong`有加粗且有强调的效果
```html
  <b>加粗的内容</b>
  <strong>加粗的内容</strong>
```


### 倾斜
* 相同点：视觉效果一样，都可以倾斜
* 不同点，`i`是单纯的倾斜，`em`有倾斜且有强调的效果
```html
  <i>倾斜的内容</i>
  <em>倾斜的内容</em>
```


### 其他标签
```html
  <sup></sup>  <!-- 上标 -->
  <sub></sub>  <!-- 下标 -->
  <br/>        <!-- 强制换行 -->
  <hr/>        <!-- 水平线，放大看是双边框哦 -->
``` 


### 特殊字符
```html
  &nbsp;  <!-- 空格 -->
  &copy;  <!-- 版权 -->
  &reg;   <!-- 商标 -->
  &lt;    <!-- 左尖括号 -->
  &gt;    <!-- 右尖括号 -->
``` 


### 列表

#### 无序列表
* 默认的符号样式，是实心圆`disc`，`type`可修改为：`circle`、`square`、`none`
```html
  <ul type="disc">
    <li>无序列表</li>
    <li>无序列表</li>
  </ul>
``` 

#### 有序列表
* 默认的符号样式，是数字 `1,2,3,4.....`
* `type`可改为：`1`、`A`、`a`、`I`、`i`
* `start`定义开始的位置，`start="3"` `type="A"` 是从`C`开始的
```html
  <ol  type="A" start="3">
    <li>有序列表</li>
    <li>有序列表</li>
  </ol>
``` 

#### 自定义列表
* `dt`规范上只有1个，`dd`可以有多个
```html
  <dl>
    <dt>可以是文字也可以图</dt>
    <dd>相关文字</dd>
  </dl>
``` 

### 图片
* `src` 图片路径
  - 相对路径
    - `./` 当前目录
    - `../` 上一级目录
  - 绝对路径
    - 存放的位置路径
    - 网络上的网址

* `width` 图片宽度
* `height` 图片高度
* `title` 鼠标悬浮的提示文字
* `alt` 图片加载失败的文字

```html
  <img src=""  width="" height="" title=""  alt=""/>
```


### 超链接
* 可以做跳转的效果
* `href` 要跳转的目的地，相对/绝对路径
* `title` 鼠标悬浮的提示文字
* `target` 窗口打开方式，`_self`默认，`_blank`新窗口打开

```html
  <a href=""  title=""  target=""></a>
```


### 表格
* 用处：做数据统计/数据展示
* 相关属性
  - 宽度 `width`
  - 高度 `height`
  - 边框 `border`
  - 边框颜色 `bordercolor`
  - 背景颜色 `bgcolor`   

* 文字对齐
  - 水平 `align="left/right/center"`
  - 垂直 `valign="top/bottom/middle"`

* 间距 加在`table`
  - 单元格和单元格的间距 `cellspacing`
  - 单元格和内容的间距 `cellpadding`

* 合并单元格
  - 合并行 `rowspan`
  - 合并列 `colspan`
  - **注意**：需要把多余的单元格删除

```html
  <table>  <!-- 创建表格 -->
      <tr>  <!-- 行 -->
      <td>1</td>  <!-- 单元格 -->
      <td>2</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
    </tr>
  </table>
```


### 表单

* 用处：收集用户数据

```html
  <form  method=""  action=""></form>
```

* 相关属性
  - `method="get/post"`，用来定义表单提交的方式
  - `action="地址"`，设置最终数据提交的目的地
  - **面试题**：`get与post的区别`
  ```md
    1- get是从服务器上获取数据，post是向服务器传送数据。
    2- get在数据传送的时候，用户可以在url上看到传递的过程，post用户是看不见的
    3- get安全性比较低，post相对来说比较高
    4- get传送的数据量比较小，post是没限制
    5- 地址栏仅识别urlencode，get在地址栏会被转码
  ```


#### 输入框
* `type`
  - 文本框 `type="text"`
  - 密码框 `type="password"`
  - 提交按钮 `type="submit"`，是按钮的形状，并有提交功能
  - 单纯的按钮 `type="button"`，没有提交功能
  - 重置按钮 `type="reset"`

* `name`
  - 名字，用来最后提交的时候，拿数据的

* `value`
  - 输入框的值

* `placeholder`
  - 设置输入框内的提示信息

```html
  <input  type=""  name=""  value="" placeholder=""/>
```

## 继续探索
>  [首页](/) | [HTML](/base/html/) | [CSS](/base/css/) | [JavaScript](/base/js/) | [QA](/base/QA/)


<hr>
<!-- 更新日期 -->

Powered by [docsify](https://docsify.js.org/) <span>|</span>
Update: {docsify-updated} 
