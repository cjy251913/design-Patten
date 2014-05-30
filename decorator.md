装饰者模式
==================

##大概定义
动态地给一个对象添加一些额外的职责，比子类更加灵活  
其实就是个接口

##例子
>比如你要买macbook，要给它的壳做雕刻engraving，要给它装虚拟机parallels，要加4G或者8G的内存。  
如果用子类实现的话，它们的全部组合要4+3+2+1=10个子类才能满足。  
而用装饰者模式只要4个接口就好了。

>如果把这些方法绑定在类上，就拔不下来了(开放-封闭原则：不能修改原代码)。  
比如一个Person，要给它穿衣服。如果给它+衬衫，+西装，+皮鞋，这些方法就永远地绑在Person上了。等下想实例化一个运动装person，还会从Person上继承衬衫，西装这些方法。根本不需要。    
Q：如果全部实例化到子类呢，西装person增加西装方法，运动装person增加运动装方法？  
A：那就不能把所有的衣服都摆出来了(放到Person上)，只能要实例化的时候给实例穿上。这很不方便。不能list所有服饰

##代码
1.子类化的方法
[代码](/decorator1.html)
    
    function vehicle(vehicleType){
        this.type = vehicleType ||"car";
        this.brand = "dafault";
        this.license = "0000-000";
  }

      //测试
      var testInstance = new vehicle("car");
      console.log(testInstance);
>vehicle {type: "car", brand: "dafault", license: "0000-000"} 

      //创建一个truck
      var truck = new vehicle("truck");
      truck.setBrand = function(brand){
         this.brand = brand;
      }
      truck.setColor = function(color){
         this.color = color;
      }

      //执行赋值
      truck.setBrand("dongfeng");
      truck.setColor("lanse");

      console.log(truck);
>vehicle {type: "truck", brand: "dongfeng", license: "0000-000", setBrand: function, setColor: function…}
brand: "dongfeng"
color: "lanse"
license: "0000-000"
setBrand: function (brand){
setColor: function (color){
type: "truck"
__proto__: vehicle

      var car = new vehicle("car");
      console.log(car);
>vehicle {type: "car", brand: "dafault", license: "0000-000"} 

2.装饰者模式
[代码](/decorator2.html)
    
    /**
    Code copyright Dustin Diaz and Ross Harmes, Pro JavaScript Design Patterns.
    **/
 
    // Constructor.用来实例化一个接口，把接口名字和方法扔进去
    var Interface = function (name, methods) {
            if (arguments.length != 2) {
                throw new Error("Interface constructor called with " + arguments.length + "arguments, but expected exactly 2.");
            }
            this.name = name;
            this.methods = [];
            for (var i = 0, len = methods.length; i < len; i++) {
                if (typeof methods[i] !== 'string') {
                    throw new Error("Interface constructor expects method names to be " + "passed in as a string.");
                }
                this.methods.push(methods[i]);
            }
        };

     
    // Static class method. 这里将一个实例化接口interface绑定要一个实例化对象object上
    Interface.ensureImplements = function (object,interface) {
        if (arguments.length < 2) {
            throw new Error("Function Interface.ensureImplements called with " + arguments.length + "arguments, but expected at least 2.");
        }
        for (var i = 1, len = arguments.length; i < len; i++) {
            var interface = arguments[i];
            if (interface.constructor !== Interface) {
                throw new Error("Function Interface.ensureImplements expects arguments" + "two and above to be instances of Interface.");
            }
            for (var j = 0, methodsLen = interface.methods.length; j < methodsLen; j++) {
                var method = interface.methods[j];
                if (!object[method] || typeof object[method] !== 'function') {
                    throw new Error("Function Interface.ensureImplements: object " + "does not implement the " + interface.name + " interface. Method " + method + " was not found.");
                }
            }
        }
    };  


