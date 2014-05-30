构造者模式
================

##定义
>将一个复杂对象的构建和它的表示分离，使得同样的构建过程可以创建不同的表示

##例子
>如果一道菜的细节是依赖于厨师，那可能会发生厨师忘记放盐这种事。这证明了"依赖倒转原则"——抽象不依赖于细节，细节依赖于抽象.  
所以，一道菜应该依赖于流程的抽象 —— 下锅，放盐，放调料，出锅.....把这些都弄成一个构造器，每次煮一道菜只要依照流程结构来执行就好了

##代码
[代码](/constructor.html)
1.对象构造
    
    //创建空对象
    1)var Person = {};
    2)var Person = new Object();
    3)var Person = Object.create(null)；  //EMCAScript

    //给对象赋予键值   1)2)属于ECMAScript3 3）属于EMCAScript5
    1）Person.name = "wuming";
       Person.prototype = {
           eat:function(){
            alert(I can eat);
           },
           sleep:function(){
            alert(I can sleep);
           }
       }
    2）Person["name"] = "wuming";
    3）Object.defineProperty(Person,"name",{
          value:"wuming",
          writable:true,    //在严格属性下，这些是有用的
          configurable:true,
          enumerable:true
        });

        Object.defineProperties(Person,{
            "name": {
                value:"wuming",
                writable:true
            },
            "anotherName": {
                value:"doudou",
                writable:true
            }
        });

    //实例化
    1）支持Object.create()
    var driver = Object.create(Person);
    driver.name = "laowang";
    console.log(driver.name);//laowang
    driver.eat();  //I can eat;
    2) 不支持Object.create();
    忘了


       

2.构造函数

    function Person(name){
        this.name = name;
    }

    Person.prototype = {
        eat:function(){
            alert(I can eat);
        },
        sleep:function(){
            alert(I can sleep);
        }
    }

    //实例化就不写了


##严格模式中，数据属性的作用
(哪天请加工下，关于严格模式和writable,configurable, enumerable)
[代码](/constructor-strict.html)

##重写超类原型会导致constructor变化
[代码](/constructor-rewrite.md)
