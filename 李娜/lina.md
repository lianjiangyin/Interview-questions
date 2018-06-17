1. ele.getAttribute('propName') 和 ele.propName区别
ele.getAttribute('propName')：是标准的DOM操作文档元素属性的方法，具有通用性可在任何文档上使用，返回值是文档元素设置的值，类型是字符串或者null（有的实现返回""）
ele.propName：通常是HTML文档中访问特点元素的特性，，这些对象的特性会根据特定规则结合属性设置得到，没有的只能用getAttribute进行访问，返回值可能是字符串，布尔值，对象，undefined
2. mouseover和mouseenter的区别
mouseover：属于划过事件，从父元素进入到子元素，属于离开父元素out，进入子元素mouseover
mouseenter：从父元素进入到资源税，斌不算离开父元素，不会触发父元素的leave，触发子元素mouseenter
mouseover存在冒泡传播，而mouseenter阻止了冒泡传播
3. 什么是事件代理
利用事件冒泡传播机制，我们只需要给容器的绑定事件即可，这样不管点击哪个后代元素，都会根据冒泡传播机制，把容器的事件行为触发，我们只需要判断事件源就可以知道点击的是谁，从而做不同的事情
4. localStorage和cookie的区别，cookie和session的关系！
cookie:存储在客户端的，每次HTTP发送请求是，客户端都会发送cookie信息到服务端。他的过期时间可以任意设置，如果不手动清除它，在它过期之前还是可以保留的。每条cookie的存储空间为4k。cookie 以名/值对形式存储
localStorage:主要是用来本地存储来使用的,可以将第一次请求的数据直接存储到本地。还解决了cookie存储空间不足的问题
cookie和session的关系:cookies是属于session对象的一种。但有不同，Cookies不会占服务器资源，是存在客服端内存或者一个cookie的文本文件中；而“Session”则会占用服务器资源。
5. 什么是闭包，你在项目中哪一块用到了闭包！
闭包：函数执行会形成一个不销毁的私有作用域，保护里面的第有变量不被外界干扰。(闭包有两个作用，保护和保存)
封装插件的时候、一些公用的方法，利用闭包的机制封装起来，这样使用的时候直接调取即可，项目中的全局变量和私有变量的污染问题用闭包来解决
6. js中定义函数的方式有哪些，区别是什么！
有三种定义函数的方式：1）函数声明，用function关键字直接定义函数,function fn(){}。2）函数定义表达式，var f=function(){}。3）使用Function()构造函数定义，var f=new function('x','return x+1')
区别：1）浏览器会先声明和定义关键字function，并在执行任何代码之前可以访问。2）表达式必须等到浏览器执行到它所在的位置代码才会真正执行。3)Function()构造函数每次执行时都会解析函数主体，并创建一个新的函数对象
7. 说出你掌握的继承方式及优缺点，并加以改进！
1）原型继承
	1、方式：子类的原型指向父类的实例  父类的实例本身就具备私有的属性和方法，子类的原型指向它，那么子类的实例就可以找到这些属性方法了
	2、和传统后台语言的继承不一样，子类继承父类并不是把父类的属性方法克隆一份副本给子类，这样处理子类和父类就没有这些关系了，JS中的原型继承是让子类和父类建立原型连接的机制，子类的实例调取父类原型上的方法都是基于原型链机制完成的。
	存在的问题：子类可以重写父类原型上的方法，子类和父类还有关系的。
原型继承存在的问题：
	1父类实例私有的属性以及公有的属性都变为子类实例的公有的属性
	2如果子类的原型上之前有属性方法，重新指向父类的子类后，之前的方法都没有了。
2）call 继承
	把A作为类创建它的实例
	把父类A作为普通函数执行，让A中的this变为B的实例，相当于给B的实例增加一些属性和方法。(弊端:把父类A当做普通函数执行，和原型A没啥关系了，仅仅是把A中的私有属性变为子类B实例的私有属性而已，A原型上的公有属性和方法和B的实例没啥关系)
3）寄生组合继承：
	A的私有变为B的私有，A的公有变为B的公有。
	基于call的继承把A的私有变为B的私有
	Object.creater
    内置object类天生自带的方法
    1创建一个空对象
    2让新创建的空对象的 _ _ proto _ _ 指向第一个传递的对象，作为新创建空对象的原型
和原型继承的区别
    B.prototype=new A();创建的A的实例虽然指向A的原型，但是实例中的不是空的，存放了A的私有属性，这些属性变为B的公有属性
    B.prototype=Object.creater(A.prototype);好处在于我们创建了一个没有私有属性和方法空对象，指向A的原型，这样B的共有就不会有A的私有属性和方法
4）ES6中的类和继承
    ES6中创建类是有自己标准语法的(这种语法创建的类只能new执行，不能当普通函数执行)
  static AA(){} //把FN当做一个普通对象设置的私有方法(和实例没有关系)，但是也只能写方法不能写属性。
8. 说出ES6和ES5的区别！
    1)扩展运算符(...)替代ES5 apply()方法
    2)Array.from()替代ES5的call()方法,将类对象转换成数组
    3)Array.of()将数值转换成数组,代替ES5 Array()方法
    4)findIndex()对比ES5 indexOf()
9. 阐述JS中的同步编程和异步编程，以及你在项目中是如何来使用异步操作的！
    同步编程：任务是按照顺序依次执行的，当前这件事没有彻底做完，下一件事是执行不了的
    异步编程：当前这件事没有彻底完成，需要等待一段时间才能继续处理，此时我们不等，继续执行下面的任务，当前的任务完成后，再去把没有彻底完成的事情完成
10. 实现一个Promise
```javascript
class Promise {
        constructor(excutorCallBack) {
            this.status='pending';
            this.value=undefined;
            this.fulfilledAry=[];
            this.rejectedAry=[];
            let resolveFn = result => {
                let timer=setTimeout(()=>{
                    if(this.status!=='pending')return;
                    clearInterval(timer);
                    this.status='fulfilled';
                    this.value=result;
                    this.fulfilledAry.forEach(item=>item(this.value))
                },0)
            };
            let rejectFn = reason => {
                let timer=setTimeout(()=>{
                    if(this.status!=='pending')return;
                    clearInterval(timer);
                    this.status='fulfilled';
                    this.value=reason;
                    this.rejectedAry.forEach(item=>item(this.value))
                },0)

            };
            try{
                excutorCallBack(resolveFn, rejectFn)
            }catch (err){
                rejectFn(err)
            }
        }
        then(fulfilledCallBack,rejectedCallBack){
            typeof fulfilledCallBack!=='function'?fulfilledCallBack=result=>result:null;
            typeof rejectedCallBack!=='function'?rejectedCallBack=reason=>{
                throw new Error(reason instanceof Error? reason.message:reason);
            }:null;
            return new Promise((resolve,reject)=>{
                this.fulfilledAry.push(()=>{
                    try{
                        let x=fulfilledCallBack(this.value);
                        x instanceof Promise? x.then(resolve,reject):resolve(x);
                    }catch (err){
                        reject(err)
                    }
                });
                this.rejectedAry.push(()=>{
                    try{
                        let x=rejectedCallBack(this.value);
                        x instanceof Promise? x.then(resolve,reject):resolve(x);
                    }catch (err){
                        reject(err)
                    }
                });
            });
        }
        catch(rejectedCallBack){
            return this.then(null,rejectedCallBack)
        }
        static all(promiseAry=[]){//Promise.all
            return new Promise((resolve,reject)=>{
                let index=0,
                    result=[];
                for (let i = 0; i < promiseAry.length; i++) {
                    promiseAry[i].then(val=>{
                        index++;
                        result[i]=val;
                        if(index===promiseAry.length){
                            resolve()
                        }
                    },reject)
                }
            })
        }

    }
module.exports = Promise;
```
11. 写出项目中经常用到的性能优化方案
    1)减少HTTP请求和请求的文件大小
    2)使用异步加载，延迟加载依赖
    3)http协议缓存,离线数据缓存localStorage
    4)动画效果，能用css就不要用js
    5)减少重绘和回流
    6)减少使用闭包
    7）尽量使用事件委托
12. 从浏览器地址栏输入URL到显示页面，中间都经历了什么（尽可能写详细，最好回答出TCP的三次握手和四次挥手，以及浏览器加载页面的细节）
    1)浏览器首先向DNS域名解析服务器发送一个请求
    2)DNS反解析：根据浏览器请求地址中的域名，到DNS服务器中好到对应服务器外网
    3)通过IP，相对于的服务器发送请求（首先访问的是服务器的WEB站点管理工具：准确来说是我们基于工具在服务器上创建很多服务，当有客户访问的时候，服务器回匹配出具体请求的哪个服务）
    4)通过URL地址中携带的端口号，找到服务器上对应的服务，以及服务所管理的项目源文件
    5)服务器端根据请求地址中的路径名称，问号传参或者hash值，把客户端需要的内容进行准备和处理
    6)把准备的内容响应给客户端（如果请求的是html或者css等这样的源文件，服务器返回的是资源文件中的源代码（不是文件本身））
    7)客户端浏览器接收到服务器返回的源代码，基于自己内部的渲染引擎(内核)开始进行页面的绘制和渲染
     ->页面计算DOM结构，生成DOM tree
     ->自上而下运行代码 加载CSS等资源内容
     ->根据获取的CSS生成带样式的RENDER TREE
     ->开始渲染和绘制页面
13. 说出你所熟知的HTTP状态码！GET和POST有啥区别！
HTTP状态码：200 请求成功。301  永久转移。302  临时转移/307  临时重定向。304设置缓存。400  请求参数错误。401 无权限。404  找不到资源。407需要代理授权。413 和服务器交互的内容组原超过服务器最大限制。500位置服务器错误。503服务器超负荷
GET和POST的区别：
    GET是基于URL问号传参的方式传递给服务器信息
    POST是基于请求主体传参的方式传递给服务器
    GET一般给服务器的少，而POST是给服务器的多。GET相对不安全，POST相对安全。GET会产生不可控的缓存，POST不会
14. 什么是HTTP报文，你熟知的报文都有哪些！
    HTTP报文：客户端和服务器交互的信息
    起始行：请求起始行、响应起始行
    首部(头)：请求头(Request Headers)、响应头(Response Headers)、通用头(General)
    主体：请求主体(Request Payload/Form Data)、响应主体(Response)
15. 能说下304具体怎样实现吗？
    1)判断当前缓存是否过期，如果没有过期，那么就不会再发送请求，直接启动之前浏览器缓存下来的文件。如果过期了，会向服务器重新发送请求，但不一定就会重新拉取文件
    2)判断文件是否有更改：缓存过期，并且文件有改动，那就重新发送请求，拉取新的文件。缓存过期，文件无改动(先向服务器发送一个请求，服务器判断是都有改动)服务器会让你用之前过期的缓存。
16. 跨域是什么？http协议中如何判断跨域？如何解决跨域问题？
    同域名，同端口，同协议：有一个不同就是跨域
    解决跨域的问题：
    1)JONSP是JSON的一种使用模式
    2)window.postMessage()
    3)document.domain方法
    4)window.name方法
17. HTTP2具体内容？SDPY了解么？
    HTTP2具体内容:
    1)①:新的二进制格式，HTTP1.x的解析是基于文本。基于文本协议的格式解析存在天然缺陷，文本的表现形式有多样性，要做到健壮性考虑的场景必然很多，二进制则不同，只认0和1的组合。基于这种考虑HTTP2.0的协议解析决定采用二进制格式，实现方便且健壮。
    ②:多路复用，即连接共享，即每一个request都是是用作连接共享机制的。一个request对应一个id，这样一个连接上可以有多个request，每个连接的request可以随机的混杂在一起，接收方可以根据request的 id将request再归属到各自不同的服务端请求里面。
    ③:header压缩，如上文中所言，对前面提到过HTTP1.x的header带有大量信息，而且每次都要重复发送，HTTP2.0使用encoder来减少需要传输的header大小，通讯双方各自cache一份header fields表，既避免了重复header的传输，又减小了需要传输的大小。
    ④:服务端推送（server push），同SPDY一样，HTTP2.0也具有server push功能。目前，有大多数网站已经启用HTTP2.0，
    2)SPDY是Google开发的基于TCP的传输层协议，用以最小化网络延迟，提升网络速度，优化用户的网络使用体验。SPDY并不是一种用于替代HTTP的协议，而是对HTTP协议的增强。新协议的功能包括数据流的多路复用、请求优先级以及HTTP报头压缩。
18. HTTPS如何实现？tsl/ssl是什么？对称加密、非对称加密在什么时候、对什么数据加密？
    HTTPS是该协议通过SSL在发送方把原始数据进行加密，在接收方解密
    SSL/TLS协议的基本思路是采用公钥加密法，也就是说，客户端先向服务器端索要公钥，然后用公钥加密信息，服务器收到密文后，用自己的私钥解密。
    对称加密:指加密和解密使用相同密钥的加密算法(就是加密密钥能够从解密密钥中推算出来，同时解密密钥也可以从加密密钥中推算出来)
    非对称加密:非对称加密算法是一种密钥的保密方法,对称加密算法需要两个密钥:公开密钥和私有密钥,公开密钥与私有密钥是一对，如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密;如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密
19. DNS劫持是什么？
    DNS劫持 就是通过劫持了 DNS 服务器，通过某些手段取得某域名的解析记录控制权，进而修改此域名的解析结果，导致对该域名的访问由原 IP 地址转入到修改后的指定 IP，其结果就是对特定的网址不能访问或访问的是假网址，从而实现窃取资料或者破坏原有正常服务的目的。DNS劫持 通过篡改 DNS 服务器上的数据返回给用户一个错误的查询结果来实现的。
20. 封装一个AJAX库！
```javascript
(function (window) {
    function AJAX(options) {
        return new init(options)
    }
    let init=function (options={}) {
        let {
            url,
            method='GET',
            data=null,
            dataType='JSON',
            async=true,
            cache=true,
            success,
            error
        }=options;
        ['url','method','data','dataType','async','cache','success','error'].forEach(item=>{
            this[item]=eval(item);
        });
        this.sendAjax()
    };
    AJAX.prototype={
        constructor:AJAX,
        init,
        sendAjax(){
            this.handleData();
            this.handleCache();
            let {method,url,async,error,success,data}=this;
            let xhr=new XMLHttpRequest();
            xhr.open(method,url,async);
            xhr.onreadystatechange=()=>{
                if(xhr.readyState===4){
                    if(!/^(2|3)\d{2}$/.test(xhr.status)){
                        error&&error(xhr.statusText,xhr);
                        return
                    }
                    let result=this.handleDataType(xhr);
                    success&&success(result,xhr)
                }
            };
            xhr.send(data)
        },
        handleDataType(xhr){
            let dataType=this.dataType.toUpperCase(),
                result=xhr.responseText;
            switch (dataType){
                case 'TEXT':
                    break;
                case 'JSON':
                    JSON.parse(result);
                    break;
                case 'XML':
                    result=xhr.responseXML;
                    break;
            }
            return result;
        },
        handleCache(){
            let {url,method,cache}=this;
            if(/^GET$/i.test(method)&&cache===false){
                url+=`${this.check()}_=${+(new Date())}`;
                this.url=url;
            }
        },
        handleData(){
            let {data,method}=this;
            if(!data)return;
            if(typeof data==='object'){
                let str=``;
                for (let key in data) {
                    if(data.hasOwnProperty(key)){
                        str+=`${key}=${data[key]}&`
                    }
                }
                data=str.substring(0,str.length-1);
            }
            if(/^(GET|DETELE|HEAD|TRACE|OPTIONS)$/i.test(method)){//这些方法都属于GET系类
                this.url+=`${this.check()}${data}`;
                this.data=null;
                return;
            }
            this.data=data;//post
        },
        check(){
            return this.url.indexOf('?')>-1?'&':'?';
        }
    };
    init.prototype=AJAX.prototype;
    window.ajax=AJAX
})(window);
```