重写超类原型会导致constructor变化
====================
[代码](/constructor-rewrite.html)
1)
  
    function Person(name){
        this.name = name;
    }
    Person.prototype.getName = function(){
        return this.name;
    }

    var driver = new Person("laowang");
    console.log(driver.constructor === Person);//true
    console.log(Person.prototype.constructor === Person);//true
    console.log(Person.constructor === Object);//false

 
2)但是，重写原型后，constructor就改变指向了（注意：和上例的区别，这里不是修改而是覆盖）

    Person.prototype = {
        getName:function(){
            return this.name;
        }
    }
    console.log(Person.prototype.constructor === Person);//false
    注意，这里的driver还是上例的。constructor没改变
    console.log(driver.constructor === Person);//true
    
    而让driver重新指向现在这个Person的时候，constructor就改变成现在Person.prototype.constructor了
    var driver = new Person("laowang");
    console.log(driver.cosstructor === Person);//false

为什么呢?  
因为重写原型后，相当于

    Person.prototype = new Object({
        getName:function(){
            return this.name;
        }
    })
    console.log(Person.prototype.constructor === Object);//true
    console.log(driver.constructor === Object);//true

3)要怎么恢复呢？   
重写Person.prototype.constructor就好了

    Person.prototype.constructor === Person;
    console.log(Person.prototype.constructor === Person);//true
    console.log(driver.constructor === Person);//true

    ![图解](/img/constructor-rewrite.jpg "见图解")