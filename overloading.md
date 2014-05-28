#方法重载

##意义
>让类以统一的方式处理不同类数据。一个函数有的参数不同(参数个数，类型),可以有不同的处理方案。
>大话设计模式中说实例化一个小猫，如果在父的Cat中就定义了要起名字才能实例化，而实例化的小猫我们还没有想好名字，就无法实例化这个小猫了。等于没起名字，就不能把孩子生出来
>方法重载就是要让起名字这个功能变得灵活

##代码
###参数长度    
    function overloading1(){
        var sum = 0;
        for(var i = 0;i<arguments.length;i ++){
            sum += arguments[i];
        }
        return sum;
    }   
    
    alert(overloading1(5));
    alert(overloading1(3,4));


###参数类型
    function overloading2(ele){
        if(typeof(ele) == "number"){
            alert("number");
        }
        if(typeof(ele) == "string"){
            alert("string");
        }
    }

    overloading2("hello");