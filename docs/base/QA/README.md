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

    补充：
    5- 函数只有形参时，在函数内部使用该参数时，结果会是undefined
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

### Js运算符相关问题

> 数学运算注意点
```js
    var a = 5
    var b = '2'

    // 加法运算，如果运算中出现了字符串。  会先将变量转为String，然后拼接。
    console.log(a+b);  // '52'
    // 其他运算，会先将变量转为 Number  再计算
    console.log(a-b);  // 3
```

> 自增自减运算符，i++ 和 ++i 是什么区别？
```js
    // i++ 表示先使用，再自增
    // ++i 表示先自增，再使用

    var a = 5
    console.log(++a + a++ + a-- + a + a-- + --a);  // 35

    var b = -3
    console.log(--b + b-- + b++ + b + --b + ++b );  // -26
```

### 循环与函数

> 循环的注意点
```js
    // JS中有3种基础的循环，while、do···while、for

    // >> do···while与while的区别是什么？
    //     - 前者是无论如何先执行一次在进行判断，后者会直接进行判断。

    // >> continue 和 break 的区别是什么？
    //     - continue 是跳过本次循环
    //     - break 是直接跳出当前循环
        
    for(var i=1;i<=6;i++){
        if(i==3){
            continue;  // 吃到第三个包子的时候，包子掉地上不能吃了，接着吃后面的包子
            break;     // 吃到第三个包子的时候，已经吃饱了不能吃了，后面的包子就都不吃了
        }
        console.log("我吃第"+i+"个包子");
    }

```

> 函数的两种声明方式的区别是什么？
```js
    // 声明式
    function fn() {}
    // 赋值式
    var fn1 = function() {}

    // 两种方式定义的函数，调用方式一致：  函数名()
    // 但是  声明式可以在声明之前调用，赋值式必须在声明后调用（否则会报错： xx is not a function）
    // 原因是因为 预解析

    函数定义阶段做了哪些儿事？
        1. 先开辟一个空间，并得到空间的地址
        2. 然后把代码当成一个字符串，存放到空间里面
        3. 最后，把这个空间的地址，赋值给函数名
```

> 函数的形参与实参相关问题
```js
    + 函数的参数有两种，形参与实参，写法如下：
        // 声明式
        function fn(形参1, 形参2, 形参3···){
            // 代码
        }
        fn(实参1, 实参2, 实参3···)

        // 赋值式
        var fn2 = function(形参1, 形参2, 形参3···){
            // 代码
        }
        fn2(实参1, 实参2, 实参3···)

    + 形参
        - 形参是在函数内部可以使用的变量，在函数外部不能使用
        - 形参的值是在函数调用的时候由实参决定的
        - 如果形参未被赋值，函数内部拿到的时候，结果为undefined
    + 实参
        - 实参一般是一个具体的值，在函数调用的时候，给形参进行赋值
        - 函数内部形参的值，是由函数调用的时候，传递的实参所决定的

    + 参数个数问题
        - 形参与实参是一一对应的
        - 如果 形参 > 实参，那么多余的形参由于未赋值，结果为undefined
        - 如果 实参 > 形参，那么由于函数内部仅能使用的是形参，所以多传递的实参无用，函数内部也拿不到
    
    + 补充：arguments
        - 每一个函数内部都有一个arguments对象
        - 他可以记录函数调用的时候传递实参的信息（是个数组）
```

> 函数的`return`相关问题
```js
+ return 表示返回的意思，有两个作用：
    - 1是终断函数执行
    - 2是给函数一个返回值

    + 1 终断函数执行
        - 函数内部的代码执行顺序，是从上到下，直到全部执行完
        - 如果在中途遇到了 return，那么后面的代码就不会执行了

        function fn(){
            console.log(1)
            console.log(2)
            console.log(3)
            // 写了return 以后，后面的就不会执行与输出了
            return;
            console.log(4);
            console.log(5)
        }


    + 2 函数的返回值
        - 函数本身就是一个表达式，表达式执行都是有结果的
        - 函数执行完以后，默认是不会有结果的，结果为undefined
        - 因此，使用 return 为函数执行完毕后，提供一个结果
    
        function fun(){
            console.log(1)
            console.log(2)
            console.log(3)
            return 10;  // 为函数执行完毕后提供一个结果
        }
        var res  = fun()
        console.log(res) // 10
```

> 预解析
```js
js是解释型语言，在执行代码之前会对代码进行通读。也就是先进行预解析，然后再执行

+ 预解析的两个内容
    - 1 使用 声明式声明的函数  function fn() {}
    - 2 使用 var 声明的变量

    fn()  // 我是函数fn()
    console.log(num)  // undefined

    function fn() {
        console.log('我是函数fn()')
    }
    var num = 2022;
     
    说明：js在执行的时候，会先进行预解析
        - 在内存中声明一个变量 fn，知道里面的内容是一个函数
        - 在内存中声明一个变量 num，但不会赋值，所以是undefined

    + 预解析优先级
        - 如果函数名与变量名相同，会优先解析函数
        - 函数的预解析优先级高于变量

    console.log( func );  // 函数体
    var func = 123;
    console.log( func );  // 123
    function func() {
        console.log( 'Hello js' );
    }
```



