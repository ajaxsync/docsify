# publicTools

>  [首页](/) | [HTML](/base/html/) | [CSS](/base/css/) | [JavaScript](/base/js/)| [QA](/base/QA/)


## 常用方法封装

```js
// ====================== 随机生成一些的方法  ======================

// 生成任意两个数之间的随机数 
function getRand(min, max) {
    return parseInt(Math.random() * (max - min + 1)) + min;
}

// 生成一个随机的颜色值 十六进制
function getColor(){
    var str = "#";
    for(var i=1;i<=6;i++){
        var num = getRand(0,15);  // 生成一个0-15之间的随机数字
        var s = num.toString(16);
        str = str + s;
    }
    return str;
}

// 生成一个随机的颜色值 RGB
function randRgb(){
    return Math.floor(Math.random()*256); // 随机生成 0-255的数
}
function getColorRgb(){
    const rc = 'rgb('+randRgb()+','+randRgb()+','+randRgb()+')'
    return rc
} 


// 生成n位纯数字的随机验证码  ======================
function getRandCode(n) {
    var num = "";
    for(var i=0; i<n; i++){
        num += Math.floor(Math.random()*10)
    }
    return num;
}


// ====================== 获取数据的方法  ======================

// 获取元素的样式(行内+非行内)
/* 
    @elem 要获取样式的某个元素
    @attr 元素的某个css属性，width、color
*/
function getStyle(elem, attr){
    if(elem.style[attr]){
        // 说明该属性是在行内写的
        return elem.style[attr]
    }else{
        // 非行内样式
        if(window.getComputedStyle){
            // 兼容非IE
            return getComputedStyle(elem)[attr]
        }else{
            // 兼容IE
            return elem.currentStyle[attr]
        }
    }
}
getStyle(box, 'color')  // 获取 box盒子的 color属性



// 万能检测数据类型 
/* 
    检测数据类型，简单、复杂
    @variable 是一个数据
    @return  返回的是一个字符串类型  'string' 'number' 'boolean' 'function'...
*/
function checkType(variable){
    if(typeof variable === 'object'){
        // 可能是一个数组，可能是一个对象
        return variable.constructor.name.toLowerCase()
    }else{
        return typeof variable
    }
}

function checkType2(variable){
    // 变量使用object里面tostring方法
    let typeStr = Object.prototype.toString.call(variable)
    typeStr = typeStr.slice(typeStr.indexOf(' '), typeStr.indexOf(']'))
    console.log(typeStr)
    return typeStr.toLowerCase()
}


// 判断arr里面是否存在num这个元素
function hasArr(arr, num){
    for(var i=0; i<arr.length; i++){
        if(arr[i]==num){
            return true;
        }
    }
    return false;
}

// 判断arr里面是否存在num这个元素  使用indexOf
function isInArr(arr, ele) {
    if(arr.indexOf(ele) != -1) {
        return true;
    }else {
        return false;
    }
}

// 判断一个对象是否为空对象
 function isEmptyObj(obj) {
    let flag = true
    for (let key in obj) {
        // 如果是一个空对象不会进入里面
        flag = false
    }
    return flag
}


// 获取页面滚动的距离
function getScroll(){
    return {
        top:window.pageYOffset||document.documentElement.scrollTop||document.body.scrollTop, //向上滚动的距离
        left:window.pageXOffset||document.documentElement.scrollLeft||document.body.scrollLeft //向左滚动的距离
    }
}

```



>  [首页](/) | [HTML](/base/html/) | [CSS](/base/css/) | [JavaScript](/base/js/) | [QA](/base/QA/)

<hr>
<!-- 更新日期 -->

Powered by [docsify](https://docsify.js.org/) <span>|</span> 
Update: {docsify-updated} 