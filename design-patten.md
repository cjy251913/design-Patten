设计模式
============

*[发布/订阅模式](#PubSub)



<h2 id = "PubSub">发布/订阅模式</h2>
***思路
>这个模式中有一个topics的放事件的列表，是一个obj。
key为订阅的事件，数组中为发布时执行的fn。如
    topics = {
        "事件1"：[fn1,fn2,fn3];
        "事件2"：[fn1,fn4];
    }
订阅时，topics中若不存在要订阅的事件，就建一个事件key，然后推入函数
发布时，遍历topics中该事件的key中的数组，并全部执行
取消订阅时，遍历topics中该事件key中的数组。若存在数组中某函数和要移除的fn相同，就移除该数组

***代码

    Publish = {};
    (function(q){
        var topics = {};

        /*这个函数是一个闭包，又是匿名函数，无法获取这个主体的名字。而参数q的作用就是要传递主体。所以把功能都绑定到q这个对象上*/
        q.publish = function(topic){
            if(!topics[topic]){
                return 0;
            }
            for(var i = 0;i <topics[topic].length;i ++){
                topics[topic][i]();
            }     
        }

        q.subscribe = function(topic,fn){
            if(!topics[topic]){
                topics[topic] = [];
            }
            topics[topic].push(fn);
        }
        
        q.unsubscribe = function(topic,fn){
            if(!topics[topic]){
                return 0;
            }
            for(var i = 0;i <topics[topic].length;i ++){
                if(topics[topic][i] == fn){
                    topics[topic].splice(i,1);
                }
            }
        }
    }(Publish));

>***示例
    //订阅
        Publish.subscribe("老板来了",function(){    //这种匿名函数无法取消订阅
            console.log("别聊天了");
        })

        function stopPlaying(){
            console.log("别玩了");
        }

        Publish.subscribe("老板来了",stopPlaying);//这种函数可以取消订阅

        Publish.publish("老板来了");

    //取消订阅
        Publish.unsubscribe("老板来了",stopPlaying);

        Publish.publish("老板来了");