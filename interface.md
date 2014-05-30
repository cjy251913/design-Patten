接口
============

##意义
1.接口把隐式公共方法和属性组合起来，以封装特定功能的一个集合
2.一旦类实现了接口，类就可以支持接口所指定的所有属性和成员
3.接口不能实例化
4.一个类可以实现多个接口

##区别类和接口
类是对对象的抽象  
抽象类是对类的抽象  
接口是对行为的抽象  

##例子
>动物中叮当猫，孙悟空，猪八戒能变出东西，但不是所有的动物都可以。所以只能在这三个类上添加方法。  
将变出东西写成一个公共接口，给类实现。

代码(/interface.html)
##一个例子
    javascript 如何实现接口
    2012-02-14 14:22:56
    具体的思路大概是这样的，先定义一个接口的对象，再定义接口的方法，然后实例化对象实现这些接口。
    1.   定义Interface对象 ： 
    var Interface = function(){....}
    2.  定义接口方法，在Interface中定义Methods数组来保存这些接口方法名称。 
    var Interface = function(name,methods){
        this.name = name;
        this.methods =[];
        .......
    }
    3. 找个实例对象来实现接口。
    4.接口方法的实现验证。即验证对象的方法名有没有把接口中的方法名都实现。这里我们会给Interface一个ensureImplements 方法，施行验证。
    
     好了，现在开始抄代码：

    //Constructor.

    var Interface = function(name,methods){//定义一个接口方法，包括方法名和方法体
        if(arguments.length != 2){//如果参数的长度不等于2，则抛出错误
            throw new Error("Interface constructor called with" + arguments.length + "arguments, but expected exactly 2.");
        }
        this.name = name;//定义方法名
        this.methods = [];//定义方法体
        for(var i = 0,len = methods.length; i <len; i++){
            if(typeof methods[i] !== 'string'){
                throw new Error("接口方法的名称必须是一个字符串");
            }
            this.methods.push(methods[i]);
        }
    };

    //Static class Method

    Interface.ensureImplements = function(object){
        if(arguments.length<2){
            throw new Error("方法 Interface.ensureImplemnents 指定了" + arguments.length+ "个参数，但是期望的是2个 .");
        }
        for(var i=1,len = arguments.length; i<len; i++){
            var _interface = arguments[i];
            if(_interface.constructor !== Interface){
                throw new Error("方法 Interface.ensureImplements 期望两个或两个以上实例对象参数");
            }

            for(var j=0, methodsLen = _interface.methods.length; j<methodsLen;j++ ){
                var method = _interface.methods[j];
                if(!object[method]||typeof object[method] !== 'function'){
                    throw new Error("Function Interface.ensureImplements: object does not implements the "+_interface.name + "interface. Method "+ method + " was not found");
                }
            }
        }
    };

     这样，一个接口类就写好了，我们定义接口的方法如下：

    var myInterface = new Interface('myInterface',['methodA','methodB','methodC']);

    //这里的myInterface 是接口名称，methodA~methodC 就是定义的接口


    Next~~ 我们来实现接口~~

    /* design interface*/
    var MyInterface = new Interface('MyInterface',['A','B','C']);
    /* implements the methods of the interface*/

    var MyObject = function(name){
    this.name = name;
    }
    MyObject.prototype.A = function(){
    alert('A');
    }
    MyObject.prototype.B = function(){
    alert('B');
    }
    MyObject.prototype.C = function(){
    alert('C');
    }
    MyObject.prototype.D = function(){
    alert('another method D');
    }

    window.onload = function(){
    var myObj = new MyObject('jgx');
    Interface.ensureImplements(myObj,MyInterface);
    myObj.D();
    }



    把这些放入网页中试试

    <html>
    <head>
    <title>test</title>
    <script type="text/javascript" src="Interface.js"></script>
    <script type="text/javascript" src="implements.js"></script>
    </head>
    <body></body>
    </html>
    
