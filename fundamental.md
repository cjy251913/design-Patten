基本概念
==============

类:泛指一类事物，例：人
对象:指一个具体的事物.。例：你自己    你是属于人的。你真对于人来说就是一个实例也就是对象。
方法:指事物能做什么行为。例：你会睡觉   睡觉就是方法。
属性，字段：指事物本身拥有的属性。例：你有鼻子和眼睛  鼻子 眼睛就是属性。
函数：是实现事物行为的载体。

**并不是字段，属性就是字符串，方法才能是函数。这只是概念上的问题，不是解决上的问题**
**其实区分这些也没什么意义好像= =**

>例子
人类：
   属性：头
   属性：手
   属性：脚
   属性：身体
   属性：性别 等
   这些大家都看的到
   字段：名字
   字段：饭量
   字段：年纪  等
   这些大家都看不到
   方法： 吃饭
   方法：睡觉
   方法：聊QQ 等
    这些都是人能干什么


##代码
1.一般对象
*属性器只能放在对象外面*
[代码](/fundamental1.html)

        cat = {
            specis : "cat",     //字段
            _name :  "wuming",  //字段  要用属性器更改的加__
            _sex : "male",      //属性
            eat : function(){   //方法
                alert("I can eat fish!");
            }
        };
        Object.defineProperty(cat,"name",{  //注意这里name是没有__
                    set:function(name){
                        this._name = name;
                    },
                    get:function(){
                        return this._name;
                    }
                });
        Object.defineProperty(cat,"sex",{
                    set:function(sex){
                        this._sex = sex;
                    },
                    get:function(){
                        return this._sex;
                    }
                });
       
        cat.name = "xiaomiao";      //注意这里改写的也没有__
        console.log(cat.name);      //这里也是
        console.log(cat.sex);
        cat.eat();




2.私有属性的构造函数
>优点
*不传给后代时可以用*
>缺点
*不能用this啊T.T*
*属性器只能放在对象里面*
*而且这些属性不可以传递给后代——见[inherit](/inherit1.html)*
*而且属性器是一些高级浏览器才能用的！low的走开*
[代码](/fundamental2.html)

        function Cat(){
                var specis = "cat";    //字段
                var name = "wuming";  //字段  这里也不用this   
                var sex = "male";   //属性
                
                Object.defineProperty(this,"name",{
                        set:function(name){
                            name = name;    //没this
                        },
                        get:function(){
                            return name;
                        }
                });
                Object.defineProperty(this,"sex",{
                            set:function(sex){
                                sex = sex;
                            },
                            get:function(){
                                return sex;
                            }
                });
             }
            
            var cat = new Cat();
            cat.name = "miao";
            console.log(cat.name);


3.一个又可以兼容，又可以继承的构造函数
[代码](fundamental3.html)
*所以，属性字段写在对象里，方法写在对象原型里！*
    function Cat(){
            this.name = "wuming";
            this.age = 10;
        }

        Cat.prototype = {
            getName : function(){
                return this.name;
            },
            setName : function(name){
                this.name = name;
            },
            shout : function(){
                alert("miao");
            }
        }

        var cat = new Cat();
        cat.setName("xiaomiao");
        alert(cat.getName());