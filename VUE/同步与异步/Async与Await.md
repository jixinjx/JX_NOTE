## What Is Async/Await
Async—声明一个异步函数(async function someName(){...})

-   自动将常规函数转换成Promise，返回值也是一个Promise对象
-   只有async函数内部的异步操作执行完，才会执行then方法指定的回调函数
-   异步函数内部可以使用await


Await—暂停异步的功能执行(var result = await someAsyncCall();)

-   放置在Promise调用之前，await强制其他代码等待，直到Promise完成并返回结果
-   只能与Promise一起使用，不适用与回调
-   只能在async函数内部使用


使用小贴士：async函数完全可以看作多个异步操作，包装成的一个 Promise 对象，而await命令就是内部then命令的语法糖。

## 使用场景介绍
1、场景一，我们同时发出三个不互相依赖的请求，如果用Async/Await就显得不明智了

![](https://pic3.zhimg.com/80/v2-c3dcb5c6ef137241015d0ff25add1c3a_1440w.webp)

如上图所示，上面我们A需要2s，B需要4s，C需要3s，我们如上图所示发请求，就存在彼此依赖的关系，c等b执行完，b等a执行完，从开始到结束需要（2+3+4）9s。

此时我们需要用Promise.all()将异步调用并行执行，而不是一个接一个执行，如下所示：

![](https://pic3.zhimg.com/80/v2-2b3ee69bcc40ea61c39c08885df316e2_1440w.webp)

这样将会节省我们不少的时间，从原来的的9s缩减到4s，是不是很开心，耶~

2、场景二，我曾经遇到过一个场景，一个提交表单的页面，里面有姓名、地址等巴拉巴拉的信息，其中有一项是手机验证码，我们不得不等待手机验证码接口通过，才能发出后续的请求操作，这时候接口之间就存在了彼此依赖的关系，Async跟Await就有了用武之地，让异步请求之间可以按顺序执行。

其中不用Async/Await的写法，我们不得不用.then()的方式，在第一个请求验证码的接口有返回值之后，才能执行后续的的Promise，并且还需要一个then输出结果，如下图：

![](https://pic3.zhimg.com/80/v2-25403dfe95814f1e68898c1957965606_1440w.webp)

  

而用Async/Await的方式去写就是下面这样，我们将逻辑分装在一个async函数里。这样我们就可以直接对promise使用await了，也就规避了写then回调。最后我们调用这个async函数，然后按照普通的方式使用返回的promise。要记得容错呢~~

![](https://pic2.zhimg.com/80/v2-59549d82905a736de2faee07c6e385e5_1440w.webp)

  

以上是两个模拟简单的场景，为的是让大家容易理解Async/Await的使用，那么接下来我们看看兼容性吧~


# async和await详解

> async和await要搭配Promise使用, 它进一步极大的改进了Promise的写法

来看一个简单的场景:

```js
//假设有4个异步方法要按顺序调用
new Promise(function(resolve){
    ajaxA("xxxx", ()=> { resolve(); })    
}).then(function(){
    return new Promise(function(resolve){
        ajaxB("xxxx", ()=> { resolve(); })    
    })
}).then(function(){
    return new Promise(function(resolve){
        ajaxC("xxxx", ()=> { resolve(); })    
    })
}).then(function(){
    ajaxD("xxxx");
});  

```

语法上不够简洁, 我们可以稍微改造一下

```js
//将请求改造成一个通用函数
function request(options) {
    //.....
    return new Promise(....); //使用Promise执行请求,并返回Promise对象
}
//于是我们就可以来发送请求了
request("http://xxxxxx")
.then((data)=>{
    //处理data
})

```

然后我们再来重新改造开头的代码

```js
request("ajaxA")
.then((data)=>{
   //处理data
   return request("ajaxB")
})
.then((data)=>{
   //处理data
   return request("ajaxC")
})
.then((data)=>{
   //处理data
   return request("ajaxD")
})

```

比起之前有了不小的进步, 但是看上去依然不够简洁

**如果我能像使用同步代码那样, 使用Promise就好了**

于是, async \ await出现了

```js
async function load(){
    await request("ajaxA");
    await request("ajaxB");
    await request("ajaxC");
    await request("ajaxD");
}

await关键字使用的要求非常简单, 后面调用的函数要返回一个Promise对象
load()这个函数已经不再是普通函数, 它出现了await这样"阻塞式"的操作
因此async关键字在这是不能省略的

```

那么现在看, 这段代码变得异常清秀

代码的编写顺序

代码的阅读顺序

代码的执行顺序

全部都是按照同步的习惯来的

是不是很方便.

到这你已经学会了async和await基本使用方式

下面来简单解释一下它的工作流程

```js
//wait这个单词是等待的意思
async function load(){
    await request("ajaxA");  //那么这里就是在等待ajaxA请求的完成
    await request("ajaxB");
    await request("ajaxC");
    await request("ajaxD");
}

```

如果后一个请求需要前一个请求的结果怎么办呢?

传统的写法是这样的

```js
request("ajaxA")
.then((data1)=>{
   return request("ajaxB", data1);
})
.then((data2)=>{
   return request("ajaxC", data2)
})
.then((data3)=>{
   return request("ajaxD", data3)
})

```

而使用async/await是这样的

```js
async function load(){
    let data1 = await request("ajaxA");  
    let data2 = await request("ajaxB", data1);
    let data3 = await request("ajaxC", data2);
    let data4 = await request("ajaxD", data3);
    //await不仅等待Promise完成, 而且还拿到了resolve方法的参数
}

```

注意当一个函数被async修饰以后, 它的返回值会被自动处理成Promise对象

关于异常处理

```js
async function load(){
    //请求失败后的处理, 可以使用try-catch来进行
    try{
        let data1 = await request("ajaxA");  
        let data2 = await request("ajaxB", data1);
        let data3 = await request("ajaxC", data2);
    } catch(e){
        //......
    }
}
```