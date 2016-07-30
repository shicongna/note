#构造函数 var cat=new Cat()

```javascript
<script type="text/javascript">
        function Cat(name){
            this.name=name;
            this.sayName=function(){
                console.log("我是"+this.name);
            }
        }
        var cat1=new Cat("maomao")
        console.log(cat1.name)
        // cat1.sayName()

        function Cat(){
            console.log(this)
        }
        var cat=Cat()
        this是window对象，因为它是一个普通函数，不是构造函数
        全局变量是window对象的属性
        全局函数是window对象的方法
</script>
```
#原型对象（Cat.prototype）：公共属性和方法

```javascript
<script type="text/javascript">
// 原型链
        function Cat(name,age){
            this.name=name;
            this.age=age;
        }
        Cat.prototype.sayName=function(){
            console.log(this.name)
        }

        WhiteCat.prototype=new Cat()
        function WhiteCat(name){
            this.name=name;
        }

        WhiteCat.prototype.color="red";
        WhiteCat.prototype.showColor=function(){
            console.log("我是"+this+"颜色")
        }
        var cat=new Cat("猫王")
        var whitecat=new WhiteCat("小猫")
        cat.sayName()
        whitecat.sayName()
</script>
```

