<!-- 
* 该文件是子目录的路由默认页
* 默认不显示目录，可以设置开启侧边栏的目录显示，该文件的目录会显示在侧边栏
* 侧边栏默认显示的一级目录，是通过根目录的_sidebar.md文件定义的。
* 嵌套目录显示是从二级目录开始的，subMaxLevel: 5 能够显示到四级目录
-->

# QA
>  [首页](/) | [HTML](/base/html/) | [CSS](/base/css/) | [JavaScript](/base/js/)

## JavaScript

### 数据类型转换QA

> 什么情况下会出现undefined？
```
    1- 变量声明未赋值
    2- 使用typeof 检测一个 不存在的变量
    3- 函数未return时，执行结果为undefined
    4- 使用void操作任何值返回的都是undefined
    参考：https://blog.csdn.net/Y2919164085/article/details/121027523
```

> 什么情况下会出现NaN?
```
常发生在数据类型转换时，如：
    1- String，如果是一个非纯数字的字符串，转Number类型
    2- undefined，转Number类型
```

> 其他类型转String注意点
```
    undefined与null只能使用 String() 进行转换
    Number、Boolean可以使用 String()、toString() 进行转换

    数据.toString(进制)，转进制时，数据为Number才会生效
```

> 数学运算注意点
```js
    var a = 5
    var b = '2'

    // 加法运算，如果运算中出现了字符串。  会先将变量转为String，然后拼接。
    console.log(a+b);  // '52'
    // 其他运算，会先将变量转为 Number  再计算
    console.log(a-b);  // 3
```

