#js笔记
## js组成部分:ECMAscript Bom Dom
#ECMAscript部分

#变量
##1.变量: 字母 下划线 $开头 驼峰命名法(firstName)
##2.var 声明变量：未使用var关键字定义的变量都是全局变量
```javascript
    function rain(){
        x = 100;   //声明了全局变量x并进行赋值
    }
    rain();
    alert( x );   //会弹出100
    <!-- 这也是JavaScript新手常见的错误，无意之中留下的许多全局变量。 -->
```
## 3.变量声明提升
```javascript
    console.log(x)
    <!-- 输出结果为undefined -->
    var x=5;
    console.log(x)
   <!--  输出结果为5 -->
```
## 4.变量作用域：if for Switch 不会创建新的执行环境，函数会创建新的执行环境与作用域

#数据类型
##数据类型：对象 数字 字符串 boolean null undefined
+ 类型转换：Number String parseInt parseFloat....
                隐式转换if(){}&nbsp;== + - * /
+ 原始数据类型: 数字 字符串 boolean null undefined
+ 引用数据类型：对象
+ 原始数据类型与引用数据类型的区别：原始类型是值的比较，引用类型是所对应的对象是否相同（指针）
+ 类型检测 typeof(检测原始数据类型)  instanceof（检测隐式转换(内置对象)）

### 对象:属性的无序集合
+ 自定义对象
+ 包装对象：Number String Boolean
+ 数组对象Array()
+ 日期对象Date()
+ 数学对象Math
+ 正则表达式RegExp()

# 语句
## 顺序
## 分支 if; if else; else if; switch
## 循环语句 for; for in; while; do while
```javascript
        var num = 1;
        function count(){
            for(var i=1;i<=100;i++){
                num *= i;
                console.log(num);
            }
        }
        count()
```

# 函数 
##1.声明函数function 返回值return 形参 实参 调用函数
        return 下面的代码永远不会被执行
##2.声明函数与函数表达式
```javascript
      function fun(){
        var x=10
        return x
}
   console.log(fun()) 
   <!-- 声明函数,调用无位置限制。函数声明提升 -->
    var fun=function(){
        var x=10
        console.log(x)
}
    fun()
 <!-- 函数表达式，只能在下方调用，无提升作用 -->
```
##3.arguments对象：函数的对象，能够找出函数的实参值及个数
##4.JavaScript的作用域链
### 首先看下下面这段代码：
```
     var rain = 1;
     function rainman(){
        var man = 2;
        function inner(){
          var innerVar = 4;
          alert(rain);
        }
        inner();    //调用inner函数
     }
    rainman();    //调用rainman函数
    <!-- 观察alert(rain);这句代码。JavaScript首先在inner函数中查找是否定义了变量rain，如果定义了则使用inner函数中的rain变量；如果inner函数中没有定义rain变量，JavaScript则会继续在rainman函数中查找是否定义了rain变量，在这段代码中rainman函数体内没有定义rain变量，则JavaScript引擎会继续向上（全局对象）查找是否定义了rain；在全局对象中我们定义了rain = 1，因此最终结果会弹出'1'。
    作用域链：JavaScript需要查询一个变量x时，首先会查找作用域链的第一个对象，如果以第一个对象没有定义x变量，JavaScript会继续查找有没有定义x变量，如果第二个对象没有定义则会继续查找，以此类推。
    上面的代码涉及到了三个作用域链对象，依次是：inner、rainman、window。 -->
```

## 5.函数声明时不执行，调用的时候执行
# 关于undefined与not define
```javascript
 <!--  测试案例1  -->
console.log(a) 
<!-- 报错 ReferenceError: a is not defined --> 

<!-- 测试案例2  -->
var a 
console.log(a) 
<!-- 无报错，但是输出undefined  -->

<!-- 测试案例2  -->
var b = {}; 
console.log(b.a) 
<!-- 无报错，但是输出undefined  -->

<!-- 测试案例3  -->
function c() { 
} 
var d = new c(); 
console.log(d.a) 
<!-- 无报错，但是显示undefined  -->
```
##总结： undefined可以翻译成：不明确的，也就是不知道用来干嘛的 
 而 not defined 可以翻译成 未定义的
