继承
===============

##继承三句话
1.子类拥有父类非private的属性和功能
2.子类具有自己的属性和功能
3.子类还可以以自己的方式实现父类的功能

###对于第一句话
[代码](inherit1.html)
可以看出，littleCat继承了Cat，但是那些属性都是Cat的私有属性，littleCat用不了
*好吧其实littleCat对于Cat，从逻辑上应该是实例化。这里用来做继承的例子了。有时间再改*

            function Cat(){
                var specis = "cat";    //字段
                var name = "wuming";  //字段    
                var sex = "male";//属性
                
                Object.defineProperty(this,"name",{
                        set:function(name){
                            name = name;
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
            console.log(cat.name);  //miao
            
            function littleCat(){}
            littleCat.prototype = new Cat();
            alert(littleCat.sex);   //underfined