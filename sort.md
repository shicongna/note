#网页类：切图，排版，特效  H5移动端 
#系统类：系统管理，数据管理 (编辑 增加 删除 排序等算法)，事件委托

##事件委托(把子集的事件委托给父级处理)
```html
    <ul id="list">
        <li>香蕉 <span class="del">删除</span></li>
        <li>苹果 <span class="del">删除</span></li>
        <li>草莓 <span class="del">删除</span></li>
    </ul>
```
```javascript
<!-- jquery事件委托 -->
<script type="text/javascript" src="script/jquery.js"></script>
    <script >
        $("#btn").click(function(){
            var val=$("#txt").val()
            var $li=$("<li></li>")
            var $span=$("<span class='del'> 删除</span>'")
            $li.text(val)
            $li.append($span)
            $("#list").append($li)
        })
        $("#list").delegate(".del","click",function(){
            $(this).parent().remove()
        })
    </script>
 <!--    js事件委托 -->
 <script type="text/javascript">
        var oTxt=document.querySelector("#txt")
        var oBtn=document.querySelector("#btn")
        var oList=document.querySelector("#list")
        oBtn.onclick=function(){
            var val=oTxt.value
            // var spanTxt=document.createTextNode("删除")
            var span=document.createElement("span")
            span.innerHTML="删除"
            span.className="del"
            var txtNode=document.createTextNode(val)
            var li=document.createElement("li")
            li.appendChild(txtNode)
            oList.appendChild(li)
            // span.appendChild(spanTxt)
            li.appendChild(span)
        }
        oList.onclick=function(event){
            var span=event.target
            if(span.className=="del"){
                this.removeChild(span.parentNode)
            }
        }
    </script>

```
##事件监听（addEventListener）:绑定相同的事件时，事件不会覆盖
```javascript
    <script type="text/javascript">
        var oBtn1=document.querySelector("#btn1")
        var oBtn2=document.querySelector("#btn2")
        var oRemove=document.querySelector("#remove")
        oBtn1.addEventListener("click",function(){
            alert("first click")
        })
        oBtn1.addEventListener("click",function(){
            alert("second click")
        })
        function fun(){
            alert("haha")
        }
        oBtn2.addEventListener("click", fun, false)
        oRemove.addEventListener("click",function(){
            oBtn2.removeEventListener("click",fun,false)
            
        })
        oRemove.addEventListener("click",function(){
            oBtn1.addEventListener("click",function(){
            alert("first click")
        })
        /*三个参数，第一个参数为事件类型，第二个参数为函数，第三个参数为boolean
        当boolean为false时，为事件冒泡，从子集到父级阶段的时候触发
        当boolean为true时，为事件捕获，从父集到子级阶段的时候触发*/
    </script>
```
## 算法
1.冒泡排序(数组元素从小到大排序)
```javascript
   <script type="text/javascript">
        var arr=[1,3,5,4,9,6]
        function sort(array){
            var len=array.length
            for(var i=len;i>=2;i--){
                for(var j=0;j<i-1;j++){
                    if(array[j]>array[j+1]){
                        var m=array[j]
                        array[j]=array[j+1]
                        array[j+1]=m
                    }
                }
            }
        }
        sort(arr)
        console.log(arr)

        function sort(array){
            for(var i=0;i<array.length;i++){
                for(var j=0;j+i<array.length-1;j++){
                    if(array[j]>array[j+1]){
                        var m=array[j]
                        array[j]=array[j+1]
                        array[j+1]=m
                    }
                }
            }
        }
        
    </script> 

```
2.顺序查找
```javascript

    var arr=[1,3,4,2,6,7,9]
    function search(array,num){
        for(var i=0;i<array.length;i++){
            if(array[i]==num){
                return i;
            }
        }
        console.log("-1")
    }
    search(arr,4)
    <!-- 找数组元素索引值 -->

    function searMax(array){
            var Max=array[0]
            for(var i=0;i<array.length;i++){
                if(array[i]>Max){
                    Max=array[i]    
                }
            }
            return Max
        }
        var result=searMax(arr)
        console.log(result)
        <!-- 找数组元素中的最大值 -->



```
3.选择排序
4.二分查找(数组元素有顺序，从小到大)
```javascript
    <script>
        var arr = [1,3,6,7,9,11,15,21,22,35,55,67,88,99];
        function search(array,data){
            var low = 0;
            var up = array.length - 1;
            var index = -1;
            (function(){
                var mid = Math.floor((low + up)/2);
                if(low<=up){
                    if(array[mid]>data){
                        up = mid -1;
                        arguments.callee();
                    }else if(array[mid]<data){
                        low = mid + 1;
                        arguments.callee();
                    }else{
                        index = mid;
                    }
                }
            })()
            return index;
        }
        console.log(search(arr,3));
        // 递归方法

        // 循环方法
        // function search(array,data){
        //  var low = 0;
        //  var up = array.length-1;
        //  while(low<=up){
        //      var mid = Math.floor((low + up)/2);
        //      if(array[mid]<data){
        //          low = mid + 1;
        //      }else if(array[mid]>data){
        //          up = mid - 1;
        //      }else{
        //          return mid;
        //      }
        //  }
        //  return -1;
        // }



    </script>

```
5.表格(综合)
```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <link rel="stylesheet" type="text/css" href="style/bootstrap.css">
</head>
<body>
    <table class="table table table-striped">
        <input type="button" id="btn1" value="年龄排序">
        <input type="button" id="btn2" value="成绩排序">
        <thead>
            <th>姓名</th>
            <th>年龄</th>
            <th>成绩</th>
        </thead>
        <tbody>   
        </tbody>
    </table>
</body>

```
```javascript
    <script type="text/javascript" src="script/jquery.js"></script>
    <script type="text/javascript">
        var arr=[
            {
                name:"小赵",
                age:"12",
                grade:99
            },
            {
                name:"小钱",
                age:"15",
                grade:92    
            },
            {
                name:"小孙",
                age:"18",
                grade:91
            },
            {
                name:"小李",
                age:"13",
                grade:88
            },
            {
                name:"小明",
                age:"14",
                grade:87
            },
            {
                name:"小亮",
                age:"11",
                grade:81
            }
        ]
        show(arr)
        $("#btn1").click(function(){
            age()
            show(arr)
        })
        $("#btn2").click(function(){
            grade()
            show(arr)
        })
        function show(array){
            $("body tbody").empty()
            for(var i in array){
                var $tr=$("<tr></tr>");
                for(var j in array[i] ){
                    var $td=$("<td></td");
                    var test=array[i][j]
                    $td.text(test)
                    $tr.append($td)
                }
                $("table tbody").append($tr)
            }
        }

        function bubbleSort(array,member){
            var len=array.length;
            for(var i=len;i>=2;i--){
                for(var j=0;j<i-1;j++){
                    if(array[j][member]>array[j+1][member]){
                        var m=array[j]
                        array[j]=array[j+1]
                        array[j+1]=m
                    }
                }
            }
        }
        
        function age(){
            bubbleSort(arr,"age")
        }
        function grade(){
            bubbleSort(arr,"grade")
        }
    </script>


    <!-- 封装   .js-->
.html里script部分
<script type="text/javascript">
        
        show(arr.data)
        $("#btn1").click(function(){
            arr.age()
            show(arr.data)
        })
        $("#btn2").click(function(){
            arr.grade()
            show(arr.data)
        })
        function show(array){
            $("table tbody").empty()
            for(var i in array){
                var $tr=$("<tr></tr>");
                for(var j in array[i] ){
                    var $td=$("<td></td");
                    var test=array[i][j]
                    $td.text(test)
                    $tr.append($td)
                }
                $("table tbody").append($tr)
            }
        }
    </script>
.js部分
var arr=(function(){
    var data=[
            {
                name:"小赵",
                age:"12",
                grade:99
            },
            {
                name:"小钱",
                age:"15",
                grade:92    
            },
            {
                name:"小孙",
                age:"18",
                grade:91
            },
            {
                name:"小李",
                age:"13",
                grade:88
            },
            {
                name:"小明",
                age:"14",
                grade:87
            },
            {
                name:"小亮",
                age:"11",
                grade:81
            }
        ]
        return {
            data:data,
            bubblesort:function(member){
                var len=this.data.length;
                for(var i=len;i>=2;i--){
                    for(var j=0;j<i-1;j++){
                        if(this.data[j][member]>this.data[j+1][member]){
                            var m=this.data[j];
                            this.data[j]=this.data[j+1];
                             this.data[j+1]=m;
                        }
                    }
                }
            },
            age:function(){
                this.bubblesort("age")
            },
            grade:function(){
                this.bubblesort("grade")
            }
        }
})()



```