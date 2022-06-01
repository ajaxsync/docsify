<!-- 
* 该文件是子目录的路由默认页
* 默认不显示目录，可以设置开启侧边栏的目录显示，该文件的目录会显示在侧边栏
* 侧边栏默认显示的一级目录，是通过根目录的_sidebar.md文件定义的。
* 嵌套目录显示是从二级目录开始的，subMaxLevel: 5 能够显示到四级目录
-->

# QA
>  [首页](/) | [HTML](/base/html/) | [CSS](/base/css/) | [JavaScript](/base/js/)

## JavaScript

### 类型转换

> 什么情况下会出现undefined？
```
    1- 变量声明未赋值
    2- 使用typeof 检测一个 不存在的变量
    3- 函数未return时，执行结果为undefined
    4- 使用void操作任何值返回的都是undefined
    参考：https://blog.csdn.net/Y2919164085/article/details/121027523

    补充：
    5- [函数的参数]函数只有形参时，在函数内部使用该参数时，结果会是undefined
    6- [作用域]当我们访问一个变量时，会优先在自身作用域查找，如果没有会继续向上一级作用域查找，一直找到全局作用域，如果依旧没有，会报错（xx is not defined）
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

### 运算符

#### 一元运算符

> 自增自减运算符，i++ 和 ++i 是什么区别？
```js
    // i++ 表示先使用，再自增
    // ++i 表示先自增，再使用

    var a = 5
    console.log(++a + a++ + a-- + a + a-- + --a);  // 35

    var b = -3
    console.log(--b + b-- + b++ + b + --b + ++b );  // -26
```

#### 二元运算符

> 数学运算符
```js
+ - * / %

需要注意的是：加法
    var a = 5
    var b = '2'

    // 加法运算，如果运算中出现了字符串。  会先将变量转为String，然后拼接。
    console.log(a+b);  // '52'

其他运算符
    // 其他运算，会先将变量转为 Number  再计算
    console.log(a-b);  // 3

    取余运算，一般用来判断奇数偶数，或是某个数的倍数
```

> 赋值运算符
```js
= += -= /= %=

其实：
a+=b  ==>  a=a+b
```

> 比较运算符 
```js
> = <= == ===

比较运算符实际比较的是：值（隐式转换为Number）

注意：
    * 如果比较的两边，是两个字符串，不会转Number比较
    * 而是按照字符串中对应的字符在编码表（UTF-16）中的数值的大小来进行比较的

等于的比较：
    * ==  仅比较值
    * === 即比较类型，也比较值
```

> 逻辑运算符
```js
&& || ！  // 运算符两边是布尔值进行比较

&&  表示两个条件必须同时满足，返回true
||  表示两个条件只要一个满足，返回false
！  表示取反，true变为false  false变为true
```

#### 三元运算符
```js
其实就相当于简单的判断

A ? B : C
条件 ? 表达式1 : 表达式2

如果条件满足，执行表达式1，不满足就执行表达式2
```


### 分支与循环

#### 分支
> 分支注意点
```js
// 分支也叫判断/选择
+ if else  
    单分支
        if(条件){
            // 代码
        }
    
    双分支
        if(条件){
            // 代码
        }else{
            // 代码
        }

    多分支
        if(条件) {
            // 代码
        }else if(条件) {
            // 代码
        } else if(条件) {
            // 代码
        } else {
            // 代码
        }

+ switch case
    switch (值) {
        case 场景值1：
            // 代码1;
        case 场景值2：
            // 代码3;
        case 场景值3：
            // 代码3;
        ···
        default:
            // 都不满足时执行的代码
    }

    * switch 的值与 case的场景值是全等的关系 （===）
    * 在case的代码片段中，如果没写 break 会有穿透效果

注意：
    * if 的条件是一个范围
    * switch 的条件是固定值
```


#### 循环

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

### 函数

> 函数的两种声明方式的区别是什么？
```js
函数的声明：
    // 声明式
    function fn() {}
    // 赋值式
    var fn1 = function() {}

函数调用：
    * 两种方式定义的函数，调用方式均是：函数名()
    * 区别：
        - 声明式函数可以在声明之前调用
        - 赋值式只能在声明后调用，否则会报错： xx is not a function 
        - 原因：和"预解析"有关

函数的命名：
   * 函数的命名规则与变量的命名规则相同

函数定义阶段做了哪些儿事？
    1. 先在（堆）开辟一个空间，并得到（堆）空间的地址
    2. 然后把代码当成一个字符串，存放到（堆）空间里面
    3. 最后，把这个空间的地址，赋值给函数名
    // 函数属于复杂数据类型，所以与复杂数据类型的赋值逻辑类似
```

> 函数的参数
```js
+ 函数的参数有两种，形参与实参，写法如下：
    * 声明式
        function fn(形参1, 形参2, 形参3···){
            // 代码
        }
        fn(实参1, 实参2, 实参3···)

    * 赋值式
        var fn2 = function(形参1, 形参2, 形参3···){
            // 代码
        }
        fn2(实参1, 实参2, 实参3···)

+ 形参
    - 形参是在函数内部可以使用的变量，在函数外部不能使用
    - 形参的值是在函数调用的时候由实参决定的，实参为形参赋值
    - 如果形参未被赋值，函数内部拿到的时候，结果为undefined
    - 比如：需要传递name、age两个参数，但只传了name，函数内部的age就为 undefined
+ 实参
    - 实参一般是一个具体的值，在函数调用的时候，给形参进行赋值
    - 函数内部形参的值，是由函数调用的时候，传递的实参所决定的

+ 参数个数问题
    - 形参与实参是一一对应的
    - 如果 形参 > 实参，那么多余的形参由于未赋值，结果为undefined
    - 如果 实参 > 形参，那么由于函数内部仅能使用的是形参，所以多传递的实参无用，函数内部也拿不到

+ 补充：arguments
    - 每一个函数内部都有一个arguments对象
    - 他可以记录函数调用的时候传递实参的信息（是个数组，使用arguments[index]）
```

> 函数`return`的相关问题
```js
+ return 表示返回的意思，有两个作用：
    - 终断函数执行
    - 为函数提供一个返回值

    + 1 终断函数的执行
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

+ 预解析会做什么？
    - 1 将 声明式函数 提前定义
    - 2 将 var 声明的变量 提前定义
    * 由此可以解释，为什么声明式函数可以在定义之前调用，而赋值式函数不行

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
    - 因为在JS中函数是头等公民，所以函数的预解析优先级高于变量

    console.log( func );  // 函数体
    var func = 123;
    console.log( func );  // 123
    function func() {
        console.log( 'Hello js' );
    }
```

> 作用域
```js
含义：一个变量可以起作用的范围，叫作用域

分类：全局作用域、局部作用域
    + 全局作用域是最大的作用域，如全局作用域window
        - 全局作用域声明的变量，在全局的任何地方均可使用
    + 局部作用域是定义在函数内部的
        - 每一个函数，都是一个局部作用域
        - 局部作用域声明的变量，只能在函数内部使用

变量的使用规则：
    + 访问规则
        - 当我们需要获取一个变量，就叫访问
        - 首先会在自身作用域查找，如果有就直接用，没有的话会向上一级作用域进行查找，一直找到全局作用域，如果依旧没有，就会报错（xx is not defined）
    + 赋值规则
        - 当我们需要给一个变量赋值，就需要先查找这个变量，然后再给变量赋值
        - 先会在自身作用域查找，如果有就直接赋值，如果没有会继续向上一级作用域查找，一直找到全局作用域，如果依旧没有，就会将该变量声明为全局变量，然后再赋值

```

> 递归函数
```js
含义：函数自己调用自己
    递归函数与循环类似，需要有初始化，自增，执行代码，条件判断，否找就是死递归
    
    function fn(){
        fn()   // 没有终止条件，是死递归
    }
    fn()

    示例：求任意数到1的累加和
    function getSum(num){
        if(num==1){
            return 1;  // 终止条件
        }else{
            return num + getSum(num-1)  // 终止条件
        }
    }
    getSum(100)  // 5050

Try it：求斐波那契数列的任意位置的值
```

### 对象

> 初识对象
```js
引入：
    * JS有两大数据类型
    * 简单/基本/原始数据类型、复杂/引用数据类型

含义：
    * 对象是JS中的一种数据类型，属于复杂数据类型，用来存复杂数据的
    * 以键值对的方式存储数据，里面存储的是一些数据的集合
    * 对象的{}中的每一个键，都是其内部的一个成员，他们之间互不影响
    
涉及到数据的存储方式：
    - JS存储数据有两个地方，栈和堆
    - 简单数据类型，是存储在栈里
    - 复杂数据类型，是存储在堆里，然后将堆的地址保存在栈里，通过地址再去找数据

    - 比喻1：
        * 假如对象是个房子，可以把数据存放在房子里，再把地址赋值给变量名
        * 需要取数据的时候，只要根据变量名保存的地址去内存中查找即可
    - 比喻2：
        * 栈可以理解为你能随身携带的口袋、书包、行李箱，变量可以理解为手机、钥匙···
        * 堆可以理解为你不必要或不能随身携带的，比如房子，数据可以理解为脸盆、牙刷，桌椅板凳···
        * 复杂数据类型，实际就是把数据放在一个房间里，然后你有这个房间的地址和钥匙（变量名，如obj）
        * 最后你把钥匙（obj）揣在口袋随身携带，当你需要洗脸刷牙的时候，可以拿着钥匙打开房间，找到脸盆、牙刷，洗脸刷牙即可。
    ==> 比喻是个人理解，仅供参考

对象的创建：
    + 字面量：
        - var obj1 = {}  // 直接创建一个空对象
        - var obj1 = {   // 创建一个有初始值的对象
            name: "张三",
            age: 18
        }
        
    + 内置构造函数：
        - var obj2 = new Object()  // 仅创建一个空对象

向对象中添加数据：
    + 使用点语法：obj.data = "2022-12-12"  // obj.key = value
    + 使用类数组法：obj['name'] = "李四"  // obj['key'] = value
    + key是对象的属性，value是属性值  // { key1: value1, key2: value2, ··· }

使用对象：
    + 点语法：obj.key
    + 类数组法：obj['key']
    * 注意：
        - [常用]当对象的键是一个具体的值（已知对象中有这个key），就用 obj.key
        - 若对象的键不是一个具体的值，可以使用obj['key']，但key记得加引号
        - 如形参中的arguments，使用时：arguments[index]，数字不用加引号

    * 删除数据
        - delete obj.key  // 会把对象里面某个键值对删除（属性与属性值都同时删除，不常用）
```

> 初识常用的交互
```js
// 为标签设置id后，可以直接使用id名获取该元素
    <div id="box"></div>
    box.innerHTML = "hello world"  // 可以获取这个div 并向div中写入值

+ 常用
    - 鼠标点击: onclick
    - 鼠标移入: onmouseover
    - 鼠标移出: onmouseout
    - 文本框内容改变: onchange

+ 修改内容
    - 向页面写入内容：innerText（仅转为字符串）、innerHTML（可识别html标签）
    - 改变输入框的值：元素.value = "值"
    - 修改元素的自带属性：
        * 元素.属性名 = 属性值，注意：class需改为className
        * 元素.backgroundColor = "red"，注意：如果属性名有-，改为大驼峰
```

### 数组

#### 数组基础

```js
含义：数组是一个有序的数据集合，下标从0开始

JS数据类型分类：
    + 简单数据类型：number、string、boolean、undefined、null
    + 复杂数据类型：function、object、array


数组的创建：
    + 字面量：
        - var arr = []  // 创建一个空数组
        - var arr = [1,2,3,4]  // 创建一个有内容的数组
    + 内置构造函数：
        - var arr = new Array() // 创建一个空数组
        - var arr = new Array(10) // 创建一个长度为10位的数组，值为 undefined
        - var arr = new Array(10, 56, 34) // 创建一个有内容/值的数组
        - var arr = new Array('10') // 创建一个值是字符串10的数组，参数是一个number才是数组长度

数组的length：
    - length 表示长度的意思
    - 数组有多少个值/成员，数组的长度就是多少
    - 语法：arr.length

数组的索引：
    - 索引也叫下标，常用 index 表示，是指一个数据在数组中排在哪一个位置
    - 注意: 在所有语言里面，索引都是从0开始的
    - 索引与数组长度的关系： index = length - 1
        * 如果某个元素的索引为-1，说明不是这个数组中的成员
    - 获取数组的某个元素：
        * 第一个元素是 arr[0] 
        * 最后一个元素是 arr[length-1]


引申并强调：数据类型之间存储的区别

    + JS数据类型的存储方式：栈、堆
        - 栈：存储基础数据类型
            * 直接在栈空间内存储一个数据
        - 堆：存储复杂数据类型
            * 先在堆里面开辟一个存储空间
            * 然后把数据存储在这个存储空间中
            * 最后把堆存储空间的地址赋值给栈里面的变量
    
    + 数据类型之间的比较：
        - 基本数据类型比较的是"值"，相互之间赋值时叫"值传递"
        - 复杂数据类型比较的是"地址"，相互之间赋值时叫"引用/地址传递"

    + 两种数据类型赋值举例：
        - 简单数据类型
            * 举例：
              var a1 = 10;
              var a2 = a1;
              console.log(a1==a2)  // true  
              // 将a1的值复制了一份给a2
              a1 = 20;
              console.log(a1, a2)  // 20  10
              // 即使更改了a1的值为20，a2的值依旧是10，两者互不影响

        - 复杂数据类型
            * 举例：
            var arr1 = { name: 'tim' }
            var arr2 = arr1  // 实际是将arr1的地址赋值给了arr2
            arr2.age = 20  // 实际会改变同一个地址里的值
            console.log(arr1, arr2)  // 两个打印的结果都会有 name与age属性
            console.log(arr1==arr2)  // true  比较的是同一个地址

    + 两种数据类型作为函数参数
        - 简单数据类型
            * 举例：
                var a = 10; // 1、定义了一个变量a
                function fn(b){
                    b++;  // 11   3、b=10 b++ = 11
                }
                fn(a);  // 2、将变量a的值赋值给b，相当于复制了一份给b
                console.log(a); // 10  4、b的变化不会影响a

        - 复杂数据类型
            * 举例：
                var m = [1,2,3,4];  // 1、定义了一个数组m
                function fn2(n){
                    n[n.length] = "hello" // 3、n得到的是m的地址，修改时会改变m的值
                }
                fn2(m);  //  2、m保存的是地址，所以是将地址复制了一份给n
                console.log(m);  // 4、n新增了数据，所以m的值也会变 [1,2,3,4, "hello"]


    + 我的比喻：
        - 相当于你租了一个房子，然后你同学想与你合租
        - 于是你把自己的钥匙配了一把给他
        - 所以你们都可以打开这个房子
        - 因此，如果你的同学买了一盆绿植
        - 当你回来的时候，会发现房间比之前多了一盆绿植

    + 总结：
        * 简单数据类型赋值，两者互不影响，一个变化另一个不会变
        * 复杂数据类型赋值，会受影响，一个变化另一个也会变化
```

#### 数组的常用方法

```js
【ES3中的常用方法】
首末增删：
    1 push
        * 功能:在数组末尾追加元素
        * 参数:arr.push(元素1,元素2,...)
        * 返回值:追加完以后数组的长度
        * 会改变原数组
    2 unshift
        * 功能:在数组前面追加元素
        * 参数:arr.unshift(元素1,元素2,...)
        * 返回值:追加完以后数组的长度
        * 会改变原数组
    3 shift
        * 功能:删除数组最前面的一个元素
        * 参数:arr.shift()
        * 返回值:被删除的元素
        * 会改变原数组
    4 pop
        * 功能:删除数组最后面的一个元素
        * 参数:arr.pop()
        * 返回值:被删除的元素
        * 会改变原数组


数组裁剪/反转/排序：
    5 splice
        * 功能:按照索引截取数组中的某些内容，可实现数组裁剪、删除、替换
        * 参数:arr.splice(从那个索引位置开始,截取多少个[,替换的新元素,...]),第三个参数可以不写
        * 返回值:被截取（删除）的内容的集合，是一个数组
        * 会改变原数组
        * 用法总结：
             + 独立门户，[返回值]截取后的返回值可以作为一个新的数组，使用被截取的内容
             + 扫地出门，[原数组]截取后，会改变原数组，从原数组中删除了不要的内容
             + 女娲补天，[原数组]在截取/删除的同时，还可以添加新的元素，所以相当于替换内容

    6 reverse
        * 功能:反转数组
        * 参数:arr.reverse()
        * 返回值:反转后的数组
        * 会改变原数组
            var arr1 = [1,2,3,4,5,6]
            var arr2 = arr1.reverse()  // 一般不关心返回值
            console.log(arr1);  // [6,5,4,3,2,1] 直接使用原数组
            console.log(arr2);  // [6,5,4,3,2,1]
            console.log(arr1==arr2);  // true

    7 sort
        * 功能:对数组元素进行排序
        * 参数:arr.sort([定义排序规则的函数]) 
        * 会改变原数组
        * 默认把数组元素转字符串，再按照字符串编码UTF-16进行排序
        * 补充知识：
               - 数字 < 大写字母 < 小写字母  可以参考：ASCII码表
               - 数字是字符串形式，仅比较第一位哦（范围是0-9）
        
        var arr = [21,2,15,65,87,99,32,77,45]
        arr.sort(function(){
            return a-b; // 从小到大排序
            return b-a; // 从大到小排序
        })

        举个栗子：
        // 将班级同学按照身高从大到小排序
        var myClass = [
            {
                name:"张三",
                score:100,
                weight:50,
                height:170
            },
            {
                name:"李四",
                score:10,
                weight:100,
                height:180
            },
            {
                name:"王五",
                score:20,
                weight:40,
                height:175
            },
            {
                name:"赵六",
                score:78,
                weight:120,
                height:190
            }
        ]

        myClass.sort(function(a,b){
            // 排序需要有个能够比较大小的参照，如身高、体重、成绩
            return b.height-a.height;  // a、b是对象，用点语法获取对应的值
        })


数组拼接：
    8 concat
        * 功能:把多个数组进行拼接
        * 参数:arr1.concat(arr2,arr3,...)
        * 返回值:拼接好的新数组
        * 不会改变原数组，而是产生一个新数组

        var arr1 = [1,2,3,4]
        var arr2 = ['你好','世界']
        var arr3 = arr1.concat(arr2)
        console.log(arr1);  // [1,2,3,4]
        console.log(arr2);  // ['你好','世界']
        console.log(arr3);  // [1,2,3,4,'你好','世界']


    9 join
        * 功能:把数组里的每一个元素连接起来，变成一个字符串[数组==>字符串]
        * 参数:arr.join("连接符号") ，如果不写"连接符号"，默认是逗号
        * 返回值:拼接好的字符串
        * 不会改变原数组
    
    数组拼接总结：
        * concat 是将所有数组中的元素取出，放在一个新数组并返回[新数组]
        * join 是将数组中的元素，通过连接符拼接成一个字符串并返回[字符串]
        * concat、join 都不会改变原数组


【ES5中的新增方法】
    1 indexOf
        + 作用:用来查找数组中某个元素的索引
        + 语法:arr.indexOf('要查找数组中的某个元素')
        + 返回值:找到的第一个元素的索引，数值类型，没找到返回-1

    2 lastIndexOf
        + 作用:用来查找数组中某个元素的索引，但是从后往前找
        + 语法:arr.indexOf('要查找数组中的某个元素')
        + 返回值:找到的第一个元素的索引，数值类型，没找到返回-1

    3 forEach
        + 作用:和for循环一样，用来遍历数组的
        + 语法:arr.forEach(function(item, index){
            // arr里面有几个元素，该函数就会执行几次
            // 函数里的形参item，代表本次循环到的元素的值
            // 函数里面的形参index，代表本次循环到的元素的索引
        })
    
    4 map
        + 作用:和forEach类似，只不过可以对数组的每一项进行操作，返回一个新的数组
        + 语法:arr.map(function(item, index){
            // arr里面有几个元素，该函数就会执行几次
            // 函数里的形参item，代表本次循环到的元素的值
            // 函数里面的形参index，代表本次循环到的元素的索引

            // 这个作为参数的函数可以设置返回值
            return item*2;
        })    
        + 返回值:所有val组成一个新数组，就是map函数的返回值
    
    5 filter
        + 作用:和map类似，按照我们的条件筛选数组
        + 语法:arr.filter(function(item, index){
            // arr里面有几个元素，该函数就会执行几次
            // 函数里的形参item，代表本次循环到的元素的值
            // 函数里面的形参index，代表本次循环到的元素的索引
            
            // 这个作为参数的函数可以设置返回值，不管返回值是什么，都看成布尔值
            if(item>20) {
                return true;
            }
        })
        + 返回值:所有的数组元素，返回值是true的元素保留，是false的元素去除，形成一个新数组返回



```


#### 数组的排序

```js
就是将乱序的数组，进行有序的排列。若是深层次，其实就是与算法有关了。

常用的排序：
    - 冒泡排序
    - 选择排序


冒泡排序：
    - 循环遍历数组，比较相邻两个变量的大小，如果第一个大于第二个，就互换位置
    - 第一轮循环结束，那个数组最后一个元素就是最大的
    - 然后再进行下一轮循环，即外层再嵌套一个循环
    - 外层循环控制整体循环次数，内层循环控制每次比较次数
    - 优化：外层与内层循环的总次数可以都减1

    var arr = [3,1,5,6,9,7,2,8]
    // 一共需要循环几次
    for(var j=0;j<arr.length-1;j++){
        // 每次循环，最大的放在后面
        for(var i=0;i<arr.length-j-1;i++){
            // 判断:如果数组的前一个比后一个大，就换位置
            if(arr[i]>arr[i+1]){
                var temp = arr[i];
                arr[i] = arr[i+1];
                arr[i+1] = temp;
            }
        }
    }

    >> 也可以使用 for in 循环，但要注意类型转换
    var arr = [3,1,5,6,9,7,2,8]
    for(var i in arr){
        var k = Number(i)  // i 是字符串类型，将其转为数值类型
        if(num[k]>num[k+1]) {
             var temp = arr[k];
            arr[k] = arr[k+1];
            arr[k+1] = temp;
        }
    }

选择排序：
    - 先假设最小元素的索引，如果有一个元素的索引比自己小，就替换原先的索引

    - 假设数组的第0个元素的索引是最小的元素 minIndex=0
    - 然后遍历数组，若是还有比自己小的元素，就替换 minIndex的值
    - 待数组遍历结束，找到索引最小的元素，将其换到第0个位置

    - 再进行第二轮遍历，此时假设最小元素的索引 minIndex=1
    - 然后继续遍历数组，若是有比自己小的元素，再次替换 minIndex的值
    - 待数组遍历结束，找到索引最小的元素，将其换到第1个位置


    var arr = [3,1,5,6,9,7,2,8]
    // 
    for(var j=0;j<arr.length;j++){
        var minIndex = j;
    // 1 先确定最小值的索引
    for(var i=j+1;i<arr.length;i++){
        if(arr[i]<arr[minIndex]){
            minIndex = i;
        }
    }
        // 2 交换位置，将最小值元素放在前面
        var temp = arr[minIndex];
        arr[minIndex] = arr[j];
        arr[j] = temp;
    }
```

### 遍历数组与对象
```js
遍历：就是获取数组或者是对象中的每个数据、键值对

可以使用 for和for...in循环

+ 遍历数组
    * 我们可以通过数组的索引获取数组的值
    * 其范围是从 0 到 arr.length-1
    * 使用for循环
        var arr = [1,2,3,4,5,6]
        for(var i=0;i<arr.length;i++) {
            console.log(arr[i]);  // 1 2 3 4 5 6
        }
    * 使用for...in循环
        var arr = [1,2,3,4,5,6]
        for(var i in arr) {
            // i 是索引 arr 是遍历的数组
            console.log(i);  // 1 2 3 4 5 6
        }

+ 遍历对象
    * 因为对象没有索引，所以不能使用for循环
    * 使用for...in循环
        var obj = {
            name: 'tim',
            age: 20
        }
        for(var i in obj) {
            // i 是对象的键  obj 是遍历的对象
            console.log(i,);  // name age 
            console.log(i, obj[i]);  // name tim ; age 20
        }
```

### 严格模式
```js
JS默认未开启严格模式，开启严格模式："use strict";

严格模式可以写在全局，也可以写在函数内部。
写在全局是针对所有代码进行严格检查，写在函数内部仅检查函数内部的代码。


严格模式的检查规则：
    * 声明变量必须有var关键字
          b = 20; // b is not defined

    * 函数的形参名不可以重复
          function fn(a,a){
            // "use strict";  // 为函数开启严格模式
            console.log(a,a)
          }
          fn(1,2); 
          // Duplicate parameter name not allowed in this context

    * 声明式函数，函数内部没有this
        + 在非严格模式下，声明式函数的函数内部 this是 window
        + 在严格模式下，声明式函数的函数内部 this是 undefined
            function fun(){
                console.log(this)
            }
            fun()
```


### this

```js
this 
    - 在全局指的是 window
    - 在函数内部指的是 window
    - 在时间函数指的是 事件源，绑定事件的那个元素/标签
```

### 字符串
```js
字符串的创建：
    + 字面量：var str = "你好，世界！"
    + 内置构造函数：var str = new String('hello world!')


拓展知识：
    ASCII字符集
        * 计算机只能存储：0101010 这样的二进制数据
        * 比如a-z、A-Z、0-9等内容，都是以二进制数字存储在计算机里的
        * 可以简单理解为：a-z、A-Z、0-9等内容，都有自己的编号
        * 然后计算机在存储的时候，存储的是这些编号
        * 当我们查看时，也是通过这些编号，然后解析成我们能看懂的内容
        * 因此就需要一个字符串和二进制的对照表，如ASCII码表
    
    Unicode编码
        * ASCII只有128个字符串的编码，由美国发明
        * 英文内容只是一些字母，所以够用，但对于世界是不够用的
        * 所以出现了unicode编码，也叫万国码/统一码
        * utf-8就是一种8位的unicode字符集，也是最常用的编码集
```


#### 字符串的常用方法
```js
【ES3】
    1 charAt
        + 作用:从一个字符串中返回指定索引位置的字符
        + 语法：str.charAt(索引)
        + 返回值：指定索引位置的字符，没有找到返回空字符串

    2 charCodeAt
        + 作用:从一个字符串中返回指定索引位置的字符编码
        + 语法：str.charCodeAt(索引)
        + 返回值：指定索引位置的字符编码，没有找到返回 NaN

    3 indexOf
        + 作用:返回第一次出现的字符的索引
        + 语法:str.indexOf(字符)
        + 返回值:字符的索引，没找到返回-1

    4 substring
        + 作用:返回一个字符串在开始索引到结束索引之间的一个子集
        + 语法:str.substring(startIndex[,endIndex])
            ==> 返回startIndex到endIndex之间的一个子集，不包括endIndex
            ==> 省略endIndex，返回从开始索引直到字符串的末尾的一个子集
        + 返回值:一个字符串，是被截取的部分，不会改变原字符串

    5 substr [官网即将废弃，不推荐使用]
        + 作用:返回一个字符串中从指定位置开始到指定字符数的字符
        + 语法:str.substr(startIndex[,length])
            ==> startIndex：可以是负数，表示倒数第几个
            ==> length:表示截取多少个，如果省略表示截取到最后一个字符
        + 返回值:一个字符串

    6 slice
        + 作用:提取某个字符串的一部分
        + 语法:str.slice(startIndex[,endIndex])
            ==> 返回startIndex到endIndex之间的一个子集，不包括endIndex
            ==> 省略endIndex,返回从开始索引直到字符串的末尾的一个子集
            ==> 可以取负数，表示倒数第几个，但startIndex<endIndex，如:(-5,-3)，否则结果为空
        + 返回值：返回一个新的字符串，且不会改变原字符串。
        + 可以实现"掐头去尾"的功能
            var str = '012345678'
            console.log(str.slice(1,-1)); // 1234567

    7 toLowerCase和toUpperCase
        + 作用：
            ==> toLowerCase:转小写
            ==> toUpperCase:转大写
        + 语法:
            str.toLowerCase()
            str.toUpperCase()
        + 返回值:
            ==> toLowerCase:全小写的字符串
            ==> toUpperCase:全大写的字符串

    8 String.fromCharCode
        + 作用:由指定的字符编码创建的字符
        + 语法:String.fromCharCode(字符编码)
        + 返回值：创建好的字符

        console.log(String.fromCharCode(90));  // Z

```

### Math与Date
```js
Math是js的一个内置对象，提供了一些操作"数字"的方法
Date是js的一个内置对象，提供了一些操作"时间"的方法


Math相关方法
Math不是内置构造函数

    1 random
        + 作用:返回0-1之间的随机数字
        + 语法:Math.random()
        + 返回值:0-1之间的随机数字,不包括1

    2 round
        + 作用:返回一个小数"四舍五入"变成一个整数
        + 语法:Math.round(数字)
        + 返回值:四舍五入变成的整数
        + 注意：四舍五入如果是0.5，按照正无穷方向取舍
            - Math.round(7.5) // 8
            - Math.round(-7.5) // -7

    3 abs
        + 作用:取一个数字的绝对值
        + 语法:Math.abs(数字)
        + 返回值:指定数字的绝对值

    4 ceil
        + 作用:将一个小数向上取整
        + 语法:Math.ceil(小数)
        + 返回值：向上取整的整数

    5 floor
        + 作用:将一个小数向下取整
        + 语法:Math.floor(小数)
        + 返回值：向下取整的整数

    6 max
        + 作用:求几个数的最大值
        + 语法:Math.max(num1,num2,num3,....)
        + 返回值：最大的那个数字

    7 min
        + 作用:求几个数的最小值
        + 语法:Math.min(num1,num2,num3,....)
        + 返回值：最小的那个数字

    8 PI
        + 作用:圆周率
        + 语法:Math.PI
        + 返回值：圆周率

    9 pow
        + 作用：求一个数的n次方
        + 语法:Math.pow(x,n)
        + 返回值：x的n次方

    补充：
        + 如何保留两位小数？
        var num = Math.random()*10 // 随机生成 1-10 的随机数
        num.toFixed(2)  // 保留两位小数 发生隐式类型转换 是string类型


Date相关方法

Date是js的内置构造函数，new Date()

* 不传递参数，默认返回当前时间
    var d = new Date() // Thu May 12 2022 16:49:36 GMT+0800 (中国标准时间)

* 传入一个字符串参数，返回你传递进入的时间
    new Date('2022/05/12 14:00')
    new Date('2022-5-12 14:00')
    new Date('2022.05.12')

* 传多个参数，代表 年月日时分秒
    + 两个参数：第一个表示年，第二个表示月
    + 三个参数: 第一个表示年，第二个表示月，第三个表示日
    + 四个参数: 第一个表示年，第二个表示月，第三个表示日，第四个表示小时
    + 五个参数: 第一个表示年，第二个表示月，第三个表示日，第四个表示小时，第五个表示分钟
    + 六个参数: 第一个表示年，第二个表示月，第三个表示日，第四个表示小时，第五个表示分钟,第六个表示秒
    + 注意：月是0-11，0表示1月,11表示12月

    new Date(2022,5)
    new Date(2022,5,12)


  + 将日期字符串格式转换成指定内容
        * 我们得到的字符串是Thu Mar 11 2021 09:40:24 GMT+0800 (中国标准时间)
        * 不是我想要的格式
        * 现在js提供了一些方法可以得到里面的指定内容
        1 getFullYear
            + 作用:得到指定字符串中的年份
            + 语法: date.getFullYear()

        2 getMonth
            + 作用:得到指定字符串中的月份
            + 语法: date.getMonth()
            + 月份是0-11
            
        3 getDate
            + 作用：得到指定字符串中的日期
            + 语法: date.getDate()

        4 getDay
            + 作用：得到指定字符串中的星期几
            + 语法：date.getDay()
            + 1-6表示星期一到星期六，星期天是0

        5 getHours
            + 作用：得到指定字符串中的小时
            + 语法: date.getHours()

        6 getMinutes
            + 作用：得到指定字符串中的分钟
            + 语法：date.getMinutes()

        7 getSeconds
            + 作用：得到指定字符串中的秒
            + 语法：date.getSeconds()

        8 getTime()
            + 作用：得到指定时间到格林威治时间的毫秒数
            + 1s = 1000ms
            + 格林威治时间：1970-1-1 00:00:00 
    
    获取时间差
        * 是指获取两个时间点之间相差的时间
        * 计算现在距离劳动节放假还有多久
        * var d1 = new Date()
        * var d2 = new Date('2021/5/1')
        * 两个时间点可以相减吗?
        * 不能直接相减，要: d2.getTime()-d1.getTime()
        * 但是:把时间对象 d 转number类型，相当于调用了 d.getTime()
        * 所以:d2.getTime()-d1.getTime() 可简写为: d2 - d1 [减法会隐式转换]
        * 得到的就是两个时间对象之间的时间差，单位是毫秒
```
* 封装了一些常用方法，[publicTools](base/QA/publicTools.md)


### BOM
```js
BOM(Browser Object Model):浏览器对象模型

可操作的内容：
    * 获取浏览器的窗口大小
        - innerWidth 获取浏览器的宽度   //  window.innerWidth
        - innerHeight 获取浏览器的高度  //  window.innerHeight
        - 宽度与高度是包含滚动条的  // 页面宽度/高度=内容区+滚动条宽度/高度
        - window.onresize  // 窗口大小改变时执行
            window.onresize = function() {
                console.log("==窗口大小改变了==")
                console.log("浏览器的宽度：" + window.innerWidth)
                console.log("浏览器的高度：" + window.innerHeight)
            }

    * 操作浏览器进行页面跳转
    * 获取浏览器地址栏的信息
    * 操作浏览器的滚动条
    * 获取浏览器的信息-版本信息
    * 让浏览器出现一些弹框（alert/confirm/prompt）
    * BOM的核心对象是window对象，里面有各种操作浏览器的方法


浏览器的弹出层
    1 alert:弹出提示框
        + 语法:alert("字符串")
        + 只能提示内容，只有一个确定按钮，点击确定，弹框消失
    2 confirm:弹出询问框
        + 语法:confirm("do you love me?")
        + 点击确定，返回true
        + 点击取消，返回false
    3 prompt:弹出输入框
        + 语法:prompt('输入内容提示'[,'输入框的初始值'])
        + 点击确定，返回输入的内容，字符串格式
        + 点击取消，返回null


浏览器的地址信息
    + window里面有一个对象location
    + 专门用来存储浏览器地址栏信息

    location.href
        + 该属性是专门存储浏览器地址栏的url信息
        + 会把中文变成url编码格式
        + encodeURI('源代码')  // 将中文转为url编码
        + decodeURI('%E6%BA%90%E4%BB%A3%E7%A0%81')  // 将url编码转为中文
    location.reload
        + 这个方法可以重新加载一次页面，就是刷新页面
        + 不要写在全局，不然浏览器会一直处在刷新状态
    location.assign
        + 这个方法可以加载指定页面
        + 原页面会保留在历史记录
    location.replace
        + 这个方法可以加载指定页面来替换本页面
        + 原页面不会保留在历史记录

特殊含义的变量：
    self:表示window
    top:表示window
    name:赋值的内容会变成字符串


浏览器的历史记录
    + window中有一个对象叫做history，专门存储历史记录信息的
    1 history.back()
        + 是用来回退历史记录的，就是回到上个页面，相当于浏览器中的⬅按钮
    2 history.forward()
        + 是用来前进历史记录的，就是去到下个页面，相当于浏览器中的➡按钮

浏览器的版本信息
    + window中有一个对象叫做navigator ，专门用来获取浏览器信息的，但不准确
    + navigator.userAgent   // 获取浏览器的整体信息
    + navigator.appName     // 获取浏览器的名称
    + navigator.appVersion  // 获取浏览器的版本信息
    + navigator.platform    // 获取当前计算机的操作系统


浏览器的onload事件
    + js代码是从上到下，按照顺序执行的
    + 若是把js代码提前，可能会获取不到某些变量

        如下代码会报错，btn is not defied
        因为在执行到点击事件时，btn还未定义
        <script>
            btn.onclick = function(){
                console.log('点击了按钮')
            }
        </script>
        <button id="btn">按钮</button>

    + 如果需要将js在前面写，可以使用浏览器的onload事件
        且一个页面只能写一个 window.onload
        <script>
            window.onload = function () {
                btn.onclick = function(){
                    console.log('点击了按钮')
                }
            }
        </script>


浏览器的onscroll事件
    + 该事件是当浏览器的滚动条（横/竖），滚动的时候触发，哪怕滚动一个像素
    + 滚动条的滚动包含：鼠标滚轮、鼠标拖动、键盘下键等方式
    + 前提是：页面的高度超过浏览器的窗口才会触发
        window.onscroll = function() {
           console.log('页面滚动了');
       }

浏览器滚动的距离
    + 其实浏览器没有动，只不过是页面向上走了
    + 因此，不能仅算做是浏览器的内容，其实也算是页面的内容
    + 所以，就不使用window对象，而是使用document对象

    1 scrollTop 获取的是页面向上滚动的距离
        + 有两种获取方式
            * document.body.scrollTop
            * document.documentElement.scrollTop  // documentElement就是HTML标签
        + 两个都是获取页面向上滚动的距离，区别:
            * IE 浏览器
                + 没有DOCTYPE声明时，用两个都行
                + 有DOCTYPE声明时，只能用document.documentElement.scrollTop
            * Chrome 和 FireFox
                + 没有DOCTYPE声明时，用document.body.scrollTop
                + 有DOCTYPE声明时，用document.documentElement.scrollTop
            * Safari
                + 两个都不用，使用一个单独的方法window.pageYOffset
   
    2 scrollLeft 获取的是页面向左滚动的距离
        + 有两种获取方式
            ==> document.body.scrollLeft
            ==> document.documentElement.scrollLeft
    
    // 因此，可以封装一个方法，获取浏览器滚动的距离
    function getScroll(){
        return {
            top:window.pageYOffset||document.documentElement.scrollTop||document.body.scrollTop, //向上滚动的距离
            left:window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft //向左滚动的距离
        }
    }

定时器
    * 两种:倒计时定时器、间隔定时器
1 倒计时定时器
    * 倒计时多少时间以后执行函数
    * 语法:setTimeout(要执行的函数, 多长时间以后执行)
    * 在你设定的时间以后，执行函数
    * 时间按照毫秒计算，1000就是1秒，且仅执行1次
    * 返回值:你定义的定时器是第几个定时器，数值类型

2 间隔定时器
    * 每间隔多少时间就执行一次函数
    * 语法:setInterval(要执行的函数，间隔多少时间)
    * 时间按照毫秒计算
    * 返回值:你定义的定时器是第几个定时器，数值类型
    * 只要不关闭，会一直执行

3 关闭定时器
    * timerId 其实就是某个定时器的返回值
    * 使用timerId 作为参数来关闭定时器
    * 两个方法:
        + clearTimeout(timerId)  // 关闭setTimeout定义的定时器
        + clearInterval(timerId) // 关闭setInterval定义的定时器
    * 关闭以后，定时器就不会执行

```


### DOM
```js
DOM(Document Object Model): 文档对象模型

拥有操作html中的标签的一些能力：
    + 获取一个元素
    + 移除一个元素
    + 创建一个元素
    + 添加一个元素
    + 给元素绑定事件
    + 获取元素的属性
    + 给元素添加一些css样式
    + 获取元素的css样式
    + ...


DOM的核心对象是：document对象，里面有各种操作元素的各种方法
DOM：是页面中的标签，我们通过js获取以后，就把这个对象叫做：DOM对象


获取元素
    1 getElementById
        * 通过标签的id名称获取，id是唯一的，所以获取的是一个元素

    2 getElementsByClassName
        * 通过标签的类名获取，元素的class名称可能有多个相同，所以获取的是一组元素
        * 即使获取的class只有一个，也是一组元素，只不过这一组中只有一个DOM元素而已
        * 获取的是一组元素，是一个长得和数组一样的数据结构，但不是数组，是伪数组
        * 这组数据也是按照索引排列的，所以要准确的拿到某个元素，需要用索引来获取

    3 getElementsByTagName
        * 通过标签名获取，元素标签名可能有多个元素，所以获取的是一组元素
        * 即使获取的标签名只有一个，也是一组元素，只不过这一组中只有一个DOM元素而已
        * 和getElementsByClassName一样，获取的是一组元素，是一个长得和数组一样的数据结构，但是不是数组，是伪数组
        * 这组数据也是按照索引排列的，所以要准确的拿到某个元素，需要用索引来获取

    4 querySelector
        * 按照选择器的方式获取元素，按照写css的方式来获取
        * 该方法只能获取到一个元素，是页面中第一个满足条件的元素

    5 querySelectorAll
        * 按照选择器的方式获取元素，按照写css的方式来获取
        * 该方法能够获取到一组元素，是页面中所有满足条件的元素
    
    // 打印获取的元素信息
    console.log(oneLi); // 打印的是获取到的标签
    console.dir(oneLi); // 打印的是详细信息，标签这个对象(键值对)


操作元素
    * 通过各种获取元素的方式，获取到页面中的标签
    * 然后，直接操作DOM元素的属性
    
    1 innerHTML
        * 获取 元素内部的html结构
        * 设置 元素内部的html结构
    
    2 innerText
        * 获取 元素内部的文本（只能获取到文本内容，获取不到html标签）
        * 设置 元素内部的文本
    
    3 getAttribute
        * 获取 元素标签上的某个属性（包括自定义属性）
    
    4 setAttribute
        * 设置 元素标签上的某个属性（包括自定义属性）
   
    5 removeAttribute
        * 删除 元素标签上的某个属性（包括自定义属性）
    
    6 样式
        * 元素.style.样式名 = "具体的值"
    
    7 className
        * 设置元素类名
        * 元素.className = "类名1 类名2"


操作节点
    DOM是我们html结构中一个一个的节点构成的
    标签、文本内容、注释，包括空格都是节点

DOM节点分类：
    * 元素节点  // 通过getElement...获取的
    * 属性节点  // 通过getAttribute获取的
    * 文本节点  // 通过innerText获取的


获取节点
    1 childNodes: 获取某一个节点下所有的子一级节点
        * 拿到的是一个伪数组，里面有多个节点
        * 里面可以看到不同种类的节点

          var oDiv = document.getElementsByTagName('div')
          oDiv.childNodes  // 获取到div下的所有的子一级节点

    2 children: (重点) 获取某一个节点下所有的子一级"元素节点"
        * 拿到的是一个伪数组，里面只有元素节点
    
    3 lastChild: 获取某一节点子一级的最后一个节点
        * 只获取到一个节点，不是伪数组
        * 获取的是子一级的最后一个节点
    
    4 firstChild: 获取某一节点子一级的第一个节点
        ==> 只获取到一个节点，不是伪数组
        ==> 获取的是子一级的第一个节点
    
    5 lastElementChild: 获取某一节点子一级的最后一个"元素节点"
        ==> 只获取到一个"元素节点"，不是伪数组
        ==> 获取的是子一级的最后一个"元素节点"
    
    6 firstElementChild: 获取某一节点子一级的第一个"元素节点"
        ==> 只获取到一个"元素节点"，不是伪数组
        ==> 获取的是子一级的第一个"元素节点"

    
    7 nextSibling: 获取某一个节点的下一个"兄弟节点"
    8 previousSibling: 获取某一个节点的上一个"兄弟节点"

    9 nextElementSibling: 获取某一个节点的下一个"兄弟元素节点"
    10 previousElementSibling: 获取某一个节点的上一个"兄弟元素节点"

    11 parentNode: (重点)获取某一个节点的"父节点"
    12 parentElement: 获取某一个节点的"父元素节点"


节点属性
    * 节点类型有多种，因此能够获取到不同的节点

    1 nodeType: 获取节点的节点类型，用数字表示
        * 元素节点:1
        * 属性节点:2
        * 文本节点:3

        console.log(oUl.nodeType)  // 1 元素节点
    
    2 nodeName: 获取节点名称
        * 元素节点:大写的标签名称
        * 属性节点:属性名
        * 文本节点:#text
    
    3 nodeValue
        * 元素节点: null，元素节点如果要获取元素内容使用:innerHTML/innerText
        * 属性节点:属性值
        * 文本节点:文本内容

```

### 事件
> 事件是您在编程时系统内发生的动作或者发生的事情，系统响应事件后，如果需要，您可以某种方式对事件做出回应。例如：如果用户在网页上单击一个按钮，您可能想通过显示一个信息框来响应这个动作。 ----[MDN](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events)

* 事件的组成
    + 触发谁的事件:事件源
    + 触发什么事件:事件类型
    + 触发以后做什么:事件处理函数
```js
// 获取事件源
var box = document.getElementById('#box');
// 事件类型 点击事件
box.onclick = function(){
    // 事件处理函数，事件函数里面的this是事件源
    this.innerHTML = "HELLO WORLD"
}
```

* 事件对象
当你触发了一个事件以后，对该事件的一些描述信息，例如：
    + 点击事件，你点在哪个位置，坐标是多少
    + 键盘事件，你按的是哪个按钮
    + 鼠标按键，你按的是左键？右键？滚轮？
每一个事件都会有一个对应的对象来描述这些信息，这个对象就叫做"事件对象"

* 浏览器提供了一个专用盒子：window.event，包含事件信息的所有描述
    + 如：点击事件，事件对象中就包含你点击的位置
        - 事件对象.鼠标点击的横坐标
        - 事件对象.鼠标点击的纵坐标
    + 如：键盘事件，事件对象中就包含你点击的按键
        - 事件对象.你的按键

    + 兼容性问题
        - 我们有两种获取事件对象的方法
        - 在每一个事件处理函数的形参位置，默认第一个就是事件对象
        - e = e || window.event

* 获取点击事件的光标坐标点
    - 每个点击事件的坐标点都不一样，因为每次点击的位置都不同
    - 坐标点根据坐标系有区别：
        + 相对事件源
        + 相对页面
        + 相对浏览器窗口
        + 相对你点击的元素

    - 相对坐标系不同，获取的事件对象里的属性也不同
        + 相对点击的元素：offsetX和offsetY 
            - 相对点击的元素的边框内侧开始计算的坐标
            - 坐标的参考点:鼠标点击的最小的元素单位
        + 相对浏览器窗口：clientX和clientY
            - 不管页面滚动到什么情况，都是根据窗口来计算坐标
        + 相对页面：pageX和pageY
            - 不管有没有滚动，都是相对页面的拿到的坐标点











>  [首页](/) | [HTML](/base/html/) | [CSS](/base/css/) | [JavaScript](/base/js/)

<hr>
<!-- 更新日期 -->

Powered by [docsify](https://docsify.js.org/) <span>|</span> 
Update: {docsify-updated} 