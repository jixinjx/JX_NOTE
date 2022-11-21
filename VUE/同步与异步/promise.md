## 出现原因

常见的一个场景就是ajax请求。通俗来说，由于网速的不同，可能你得到返回值的时间也是不同的，这个时候我们就需要等待，结果出来了之后才知道怎么样继续下去。
在ajax的原生实现中，利用了onreadystatechange事件，当该事件触发并且符合一定条件时，才能拿到想要的数据，之后才能开始处理数据。

这样做看上去并没有什么麻烦，但如果这个时候，我们还需要另外一个ajax请求，这个新ajax请求的其中一个参数，得从上一个ajax请求中获取，这个时候我们就不得不等待上一个接口请求完成之后，再请求后一个接口。如下：

```js
var url = 'https://hq.tigerbrokers.com/fundamental/finance_calendar/getType/2017-02-26/2017-06-10';
var result;

var XHR = new XMLHttpRequest();
XHR.open('GET', url, true);
XHR.send();

XHR.onreadystatechange = function() {
    if (XHR.readyState == 4 && XHR.status == 200) {
        result = XHR.response;
        console.log(result);

        // 伪代码
        var url2 = 'http:xxx.yyy.com/zzz?ddd=' + result.someParams;
        var XHR2 = new XMLHttpRequest();
        XHR2.open('GET', url, true);
        XHR2.send();
        XHR2.onreadystatechange = function() {
            ...
        }
    }
}
```

当出现第三个ajax(甚至更多)仍然依赖上一个请求时，我们的代码就变成了一场灾难。这场灾难，往往也被称为**回调地狱**。

因此我们需要一个叫做Promise的东西，来解决这个问题。

当然，除了回调地狱之外，还有一个非常重要的需求：**为了代码更加具有可读性和可维护性，我们需要将数据请求与数据处理明确的区分开来**。上面的写法，是完全没有区分开，当数据变得复杂时，也许我们自己都无法轻松维护自己的代码了。这也是模块化过程中，必须要掌握的一个重要技能，请一定重视。

## 什么是promise
抽象表达：Promise是JS中进行异步编程的新的解决方案（旧的是谁？===〉纯回调形式）

具体表达：

从语法上说：Promise是一个构造函数；

从功能上说：Promise对象用来封装一个异步操作并可以获取其结果；

Promise状态改变：

 

pending变为resolved 【成功】

pending变为rejected  【失败】

说明：只有这两种，且一个promise对象只能改变一次；

           无论变为成功还是失败，都会有一个结果数据；

          成功的结果数据一般称为value，失败的结果数据一般称为reason;


## 为什么要用Promise？

指定回调函数的方式更加灵活

旧的：必须在启动异步任务之前指定

promise: 启动异步任务 => 返回promise对象 => 给promise对象绑定回调函数(甚至可以在异步任务结束后指定)

支持链式调用，可以解决回调地狱问题

什么是回调地狱？回调函数嵌套调用，外部回调函数异步执行的结果是嵌套的回调函数执行的条件

回调地狱的缺点？不便于阅读 / 不便于异常处理


解决方案？ promise链式调用 **【一个Promise对应一个异步任务】**

```javascript

dosomething()
.then(result=>{
    return doSomethingElse(result)
}).then(newresult=>{
   return doSomeThingOther(finalResult)
}).then(finalResult=>{
   console.log("最终结果："+finalResult)
}).catch(failureCallBack);  //异常传透！，当以上任意一个Promise有问题，都会调用失败回调函数

```

终极解决方案？ async/await
``` JavaScript
async function request(){
    try{
     const result=await doSomething();
     const newresult=await doSomeThingElse(result);
     const finalResult=await doSomeThingOther(newresult);
     console.log("最终结果："+finalResult)
    }
}catch(error){
   failureCallBack(error);
};
```
