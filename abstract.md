抽象类
===================

##注意
1.抽象类不能实例化
2.抽象方法是必须被子类重写的方法(这句话没啥意思略过)
3.如果类中包含抽象方法，就必须被定位抽象类，不管有没有一般方法

##用途
1.抽象类拥有尽可能多的共同代码
2.继承上是树枝节点
3.图见大话设计模式p354

##代码
        
        function Animal(){}   
        Animal.prototype = {    //抽象类的原型方法
            shout:function(){
                alert(this.shoutName);  //shoutName即使还没定义都没关系。只要没调用就不会出错
            }
        }

       function Cat(name){      
            this.name = name;       //新类的属性
       }
       Cat.prototype = new Animal();    //新类从Animal那里搬来了全部东西
       /*Cat.prototype = {        //新类原型还可以再添加一些东西。但如果这样就重写原型了。从Animal那里继承来的所有东西都不见了
            shoutName : "miao"
       }
*/     
       Cat.prototype.shoutName = "miao";    //覆盖从Animal那里继承来的shouName
       var cat1 = new Cat("guapi");
       cat1.shout();  