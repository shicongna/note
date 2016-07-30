# 闭包：函数嵌套会形成一个闭包
##封装代码(以件数增加减少为例，封装代码)
```javascript
    // 利用Jquery方法封装
    (function(){
            var n=0
            var price=5.24
            function addfun(){
                n++
                var total=(n*price).toFixed(2)
                console.log(total)
            }
            function subfun(){
                n--
                var total=(n*price).toFixed(2)
                console.log(total)
            }
            window.fun=[addfun,subfun]  
        })()
        var oadd=document.querySelector("#add")
        var osub=document.querySelector("#sub")
        oadd.onclick=fun[0]
        osub.onclick=fun[1]

     // 利用函数表达式封装
        var count=(function(){
            var n=0
            var price=5.24
            function addfun(){
                n++
                var total=(n*price).toFixed(2)
                console.log(total)
            }
            function subfun(){
                n--
                var total=(n*price).toFixed(2)
                console.log(total)
            }
            return{
                add:addfun,
                sub:subfun
            }   
        })()
        var oadd=document.querySelector("#add")
        var osub=document.querySelector("#sub")
        oadd.onclick=count.add
        osub.onclick=count.sub

```

# 递归函数：自己调用自己的函数
```javascript

  function fun(x){
    if(x==1){
        return x
    }else{
        return x*fun(x-1)
    }
}
fun(5)
```
#回调函数：把一个函数当参数传递给另一个函数  ($().click(function(){}))
```javascript
    function fun(callback){
        callback()
}
    fun(function(){
     console.log("hello")
    })
```

