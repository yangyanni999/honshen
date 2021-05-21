# js笔记

## 正则表达式

**/runoob/i** 是一个正则表达式。

**runoob** 是一个**正则表达式主体** (用于检索)。

**i** 是一个**修饰符** (搜索不区分大小写)。

var str = "Visit Runoob!";  

var n = str.search(/Runoob/i);  6



var str = document.getElementById("demo").innerHTML;  

var txt = str.replace(/microsoft/i,"Runoob");

不区分大小写 microsoft替换为runoob

![image-20210520113910423](C:\Users\王贤宇\AppData\Roaming\Typora\typora-user-images\image-20210520113910423.png)



test() 方法是一个正则表达式方法。

test() 方法用于检测一个字符串是否匹配某个模式，如果字符串中含有匹配的文本，则返回 true，否则返回 false。

/e/.test("The best things in life are free!")  			true



exec() 方法用于检索字符串中的正则表达式的匹配。

该函数返回一个数组，其中存放匹配的结果。如果未找到匹配，则返回值为 null。

/e/.exec("The best things in life are free!");  		e



```javascript
/*是否带有小数*/
function    isDecimal(strValue )  {  
   var  objRegExp= /^\d+\.\d+$/;
   return  objRegExp.test(strValue);  
}  

/*校验是否中文名称组成 */
function ischina(str) {
    var reg=/^[\u4E00-\u9FA5]{2,4}$/;   /*定义验证表达式*/
    return reg.test(str);     /*进行验证*/
}

/*校验是否全由8位数字组成 */
function isStudentNo(str) {
    var reg=/^[0-9]{8}$/;   /*定义验证表达式*/
    return reg.test(str);     /*进行验证*/
}

/*校验电话码格式 */
function isTelCode(str) {
    var reg= /^((0\d{2,3}-\d{7,8})|(1[3584]\d{9}))$/;
    return reg.test(str);
}

/*校验邮件地址是否合法 */
function IsEmail(str) {
    var reg=/^\w+@[a-zA-Z0-9]{2,10}(?:\.[a-z]{2,4}){1,3}$/;
    return reg.test(str);
}
```



## 错误（异常）

```javascript
try {
    ...    //异常的抛出
} catch(e) {
    ...    //异常的捕获与处理
    // err有message和name属性
} finally {
    ...    //结束处理
}
```



## 变量提升

```javascript
var x = 5; // 初始化 x
var y = 7; // 初始化 y

elem = document.getElementById("demo"); // 查找元素
elem.innerHTML = x + " " + y;           // 显示 x 和 y



var x = 5; // 初始化 x

elem = document.getElementById("demo"); // 查找元素
elem.innerHTML = x + " " + y;           // 显示 x 和 y  y是undefined

var y = 7; // 初始化 y
```



## 严格模式

"use strict"

不能使用未声明的变量

```JavaScript
"use strict";
x = 3.14;                // 报错 (x 未定义)

Note	对象也是一个变量。

"use strict";
x = {p1:10, p2:20};      // 报错 (x 未定义)

不允许删除变量或对象。

"use strict";
var x = 3.14;
delete x;                // 报错

不允许删除函数。

"use strict";
function x(p1, p2) {};
delete x;                // 报错 

不允许变量重名:

"use strict";
function x(p1, p1) {};   // 报错

不允许使用八进制:

"use strict";
var x = 010;             // 报错

不允许使用转义字符:

"use strict";
var x = \010;            // 报错

不允许对只读属性赋值:

"use strict";
var obj = {};
Object.defineProperty(obj, "x", {value:0, writable:false});

obj.x = 3.14;            // 报错

不允许对一个使用getter方法读取的属性进行赋值

"use strict";
var obj = {get x() {return 0} };

obj.x = 3.14;            // 报错

不允许删除一个不允许删除的属性：

"use strict";
delete Object.prototype; // 报错

变量名不能使用 "eval" 字符串:

"use strict";
var eval = 3.14;         // 报错

变量名不能使用 "arguments" 字符串:

"use strict";
var arguments = 3.14;    // 报错


"use strict";
with (Math){x = cos(2)}; // 报错

由于一些安全原因，在作用域 eval() 创建的变量不能被调用：

"use strict";
eval ("var x = 2");
alert (x);               // 报错
```



## JSON

JSON 数据格式为 键/值 对，就像 JavaScript 对象属性。

键/值对包括字段名称（在双引号中），后面一个冒号，然后是值："name":"Runoob"

```JavaScript
"sites":[
    {"name":"Runoob", "url":"www.runoob.com"}, 
    {"name":"Google", "url":"www.google.com"},
    {"name":"Taobao", "url":"www.taobao.com"}
]

/*
通常我们从服务器中读取 JSON 数据，并在网页中显示数据。

简单起见，我们网页中直接设置 JSON 字符串:

首先，创建 JavaScript 字符串，字符串为 JSON 格式的数据：
*/

var text = '{ "sites" : [' +
'{ "name":"Runoob" , "url":"www.runoob.com" },' +
'{ "name":"Google" , "url":"www.google.com" },' +
'{ "name":"Taobao" , "url":"www.taobao.com" } ]}';

//然后，使用 JavaScript 内置函数 JSON.parse() 将字符串转换为 JavaScript 对象:

var obj = JSON.parse(text);


//JSON.parse()	用于将一个 JSON 字符串转换为 JavaScript 对象。
//JSON.stringify()	用于将 JavaScript 值转换为 JSON 字符串。

```



## AJAX



所有现代浏览器均支持 XMLHttpRequest 对象（IE5 和 IE6 使用 ActiveXObject）。

XMLHttpRequest 用于在后台与服务器交换数据。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。



```javascript
var xmlhttp;
if (window.XMLHttpRequest)
{
    //  IE7+, Firefox, Chrome, Opera, Safari 浏览器执行代码
    xmlhttp=new XMLHttpRequest();
}
else
{
    // IE6, IE5 浏览器执行代码
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
}
```



向服务器请求

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：

- 无法使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠



## 异步



## Promise

```javascript
//计时器 每个延迟不同的时间再启动
setTimeout(function () {
    console.log("First");
    setTimeout(function () {
        console.log("Second");
        setTimeout(function () {
            console.log("Third");
        }, 3000);
    }, 4000);
}, 1000);

new Promise(function (resolve, reject) {
    setTimeout(function () {
        console.log("First");
        resolve();
    }, 1000);
}).then(function () {
    //这个return后面有解释
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            console.log("Second");
            resolve();
        }, 4000);
    });
}).then(function () {
    setTimeout(function () {
        console.log("Third");
    }, 3000);
});

//语法格式 then可以有多个
/*
resolve 是执行成功 参数会给 then
reject 是执行失败 参数给catch
resolve 和 reject 的作用域只有起始函数，不包括 then 以及其他序列；
resolve 和 reject 并不能够使起始函数停止运行，别忘了 return*/
new Promise(function (resolve, reject) {
    var a = 0;
    var b = 1;
    if (b == 0) reject("Divide zero");
    else resolve(a / b);
}).then(function (value) {
    console.log("a / b = " + value);
}).catch(function (err) {
    console.log(err);
}).finally(function () {
    console.log("End");
});

new Promise(function (resolve, reject) {
    console.log(1111);
    resolve(2222);
}).then(function (value) {
    console.log(value);
    return 3333;
}).then(function (value) {
    console.log(value);
    throw "An error";
}).catch(function (err) {
    console.log(err);
});


//注意这个return
function print(delay, message) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            console.log(message);
            resolve();
        }, delay);
    });
}

//print(1000, "First")就是是上面函数返回的一个promise对象
print(1000, "First").then(function () {
    //这里为什么又用return？
    return print(4000, "Second");
    //意思是下一个.then其实是第二个（4000）promise的then，而不是第一个（1000）promise的then
}).then(function () {
    print(3000, "Third");
});

function print(delay, message) {
    return new Promise(function (resolve, reject) {
        setTimeout(function () {
            console.log(message);
            resolve();
        }, delay);
    });
}



print(1000, "First").then(function () {
    return print(4000, "Second");
}).then(function () {
    print(3000, "Third");
});
//我们可以将这段代码变得更好看

//async 异步函数 
//await 指令后必须跟着一个 Promise，异步函数会在这个 Promise 运行中暂停，直到其运行结束再继续运行
async function asyncFunc() {
    await print(1000, "First");
    await print(4000, "Second");
    await print(3000, "Third");
}
asyncFunc();
```

