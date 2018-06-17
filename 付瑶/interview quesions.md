
### JavaScript （前端玩家必备技能）
1. ele.getAttribute('propName') 和 ele.propName区别(https://zhidao.baidu.com/question/755671673860081724.html?)
    getAttribute()：获取的是HTML节点元素的属性（css获取）。
    返回值：返回当前元素属性名对应的属性值。类型：字符串（不是字符串会调用toString）或null
    prop() ：获取的是元素的属性值（js获取） 返回值得类型：包括数组对象在内的任意类型。
    显然prop的性能更高，因为attr需要访问DOM属性节点，访问DOM是最耗时的。这种情况适用于多选项全选和反选的情况。
    什么时候使用attr()，什么时候使用prop()？
    1.添加属性名称该属性就会生效应该使用prop();（用getAttribute添加的属性添加到元素节点中，prop获取不到）
    2.是有true,false两个属性使用prop();（checked,selected,readonly和disabled prop返回true或false. attr()返回checked/""）
    3.其他则使用attr();
2. mouseover和mouseenter的区别
    情况一：绑定两个事件的元素没有子元素时，两个方法没有区别。
    情况二：绑定两个事件的元素有子元素时。
    不论鼠标指针穿过被选元素或其子元素，都会触发 mouseover 事件。对应mouseout事件
    只有在鼠标指针穿过被选元素时，才会触发 mouseenter 事件。对应mouseleave事件
    mouseover和mouseenter其区别的本质：mouseover会冒泡。mouseenter不支持冒泡

3. 什么是事件代理（https://www.cnblogs.com/liugang-vip/p/5616484.html）
    事件代理（事件委托）：利用事件冒泡机制，指定一个事件，管理某一类型的所有事件。
    事件代理的好处：减少DOM操作，优化性能。减少冗余代码。

    那什么样的事件可以用事件委托，什么样的事件不可以用呢？
    适合用事件委托的事件：click，mousedown，mouseup，keydown，keyup，keypress。
    值得注意的是，mouseover和mouseout虽然也有事件冒泡，但是处理它们的时候需要特别的注意，因为需要经常计算它们的位置，处理起来不太容易。
    不适合的就有很多了，举个例子，mousemove，每次都要计算它的位置，非常不好把控，在不如说focus，blur之类的，本身就没用冒泡的特性，自然就不能用事件委托了。

4. localStorage和cookie的区别，cookie和session的关系！（https://www.cnblogs.com/cencenyue/p/7604651.html）
（https://blog.csdn.net/ruby_xc/article/details/65939988）
    浏览器的缓存机制提供了可以将用户数据存储在客户端上的方式，可以利用cookie,session等跟服务端进行数据交互
    一、cookie和session
    区别：
    1、保持状态：cookie保存在浏览器端，session保存在服务器端
    2、使用方式：
    （1）cookie机制：如果不在浏览器中设置过期时间，cookie被保存在内存中，生命周期随浏览器的关闭而结束，这种cookie简称会话cookie。如果在浏览器中设置了cookie的过期时间，cookie被保存在硬盘中，关闭浏览器后，cookie数据仍然存在，直到过期时间结束才消失。
         Cookie是服务器发给客户端的特殊信息，cookie是以文本的方式保存在客户端，每次请求时都带上它
    （2）session机制：当服务器收到请求需要创建session对象时，首先会检查客户端请求中是否包含sessionid。如果有sessionid，服务器将根据该id返回对应session对象。如果客户端请求中没有sessionid，服务器会创建新的session对象，并把sessionid在本次响应中返回给客户端。通常使用cookie方式存储sessionid到客户端，在交互中浏览器按照规则将sessionid发送给服务器。如果用户禁用cookie，则要使用URL重写，可以通过response.encodeURL(url) 进行实现；API对encodeURL的结束为，当浏览器支持Cookie时，url不做任何处理；当浏览器不支持Cookie的时候，将会重写URL将SessionID拼接到访问地址后。
    3、存储内容：cookie只能保存字符串类型，以文本的方式；session通过类似与Hashtable的数据结构来保存，能支持任何类型的对象(session中可含有多个对象)
    4、存储的大小：cookie：单个cookie保存的数据不能超过4kb；session大小没有限制。
    5、安全性：cookie：针对cookie所存在的攻击：Cookie欺骗，Cookie截获；session的安全性大于cookie。
    　　　　　　原因如下：（1）sessionID存储在cookie中，若要攻破session首先要攻破cookie；
    　　　　　　　　　　　（2）sessionID是要有人登录，或者启动session_start才会有，所以攻破cookie也不一定能得到sessionID；
    　　　　　　　　　　　（3）第二次启动session_start后，前一次的sessionID就是失效了，session过期后，sessionID也随之失效。
    　　　　　　　　　　　（4）sessionID是加密的
    　　　　　　　　　　　（5）综上所述，攻击者必须在短时间内攻破加密的sessionID，这很难。
    6、应用场景：
    cookie：（1）判断用户是否登陆过网站，以便下次登录时能够实现自动登录（或者记住密码）。如果我们删除cookie，则每次登录必须从新填写登录的相关信息。
    　　　　（2）保存上次登录的时间等信息。
    　　　　（3）保存上次查看的页面
    　　　　（4）浏览计数
    localStorage：数据始终有效，可以做持久数据。在所有同源窗口中共享。存储大小5M或更大


5. 什么是闭包，你在项目中哪一块用到了闭包！
    闭包就是能够读取其他函数内部变量的函数。
    由于在Javascript语言中，只有函数内部的子函数才能读取局部变量，因此可以把闭包简单理解成"定义在一个函数内部的函数"。
    所以，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。
    闭包的使用场景：
    1）通过循环给页面上多个dom节点绑定事件
    2）封装变量
    3）实现类的继承
    4）匿名自执行函数
    使用闭包的注意点
    1）由于闭包会使得函数中的变量都被保存在内存中，内存消耗很大，所以不能滥用闭包，否则会造成网页的性能问题，在IE中可能导致内存泄露。解决方法是，在退出函数之前，将不使用的局部变量全部删除。
    2）闭包会在父函数外部，改变父函数内部变量的值。所以，如果你把父函数当作对象（object）使用，把闭包当作它的公用方法（Public Method），把内部变量当作它的私有属性（private value），这时一定要小心，不要随便改变父函数内部变量的值。

6. js中定义函数的方式有哪些，区别是什么！
    1.函数声明   function(){}
    2.函数表达式  var fn = function(){}
    3.构造函数    var fn = new Function()
    4.es6 class        class fn{}
    5.匿名自执行函数    (function (){ return function () {}})()
7. 说出你掌握的继承方式及优缺点，并加以改进！
    1.原型链继承：子类的原型等于父类的一个实例（不能通过传参的方式实例化对象）
    2.类式继承： call,借用父类的构造函数实现继承（无法继承到原型对象里定义的方法）
    3.组合式继承：完美的继承了父类的所有方法和属性
    4.寄生组合继承：①创建一个没有实例的类②子类的原型等于创建类的实例（只继承父类原型上的方法）

8. 说出ES6和ES5的区别！

9. 阐述JS中的同步编程和异步编程，以及你在项目中是如何来使用异步操作的！
    同步：在一个线程上（主栈/主任务队列）同一个时间只能做一件事情，当前事情完成才能进行下一个事情（先把一个任务进栈执行，执行完成，在把下一个任务进栈，上一个任务出栈...）
   异步：在主栈中执行一个任务，但是发现这个任务是一个异步的操作，我们会把它移除主栈，放到等待任务队列中（此时浏览器会分配其它线程监听异步任务是否到达指定的执行时间）,如果主栈执行完成，监听者会把到达时间的异步任务重新放到主栈中执行...
      定时器
      事件绑定
      ajax
      回调函数
      Node中fs可以进行异步的I/O操作
      process.nextTick
      promise(async awiat)

10. 实现一个Promise

### HTTP && AJAX && 跨域 （18+玩家必备技能，初级玩家需要了解一些的）
1. 写出项目中经常用到的性能优化方案
    1)加载性能优化
    2）css优化
    3）js优化
    4）浏览器的查找顺序
    5）CDN加速
2. 从浏览器地址栏输入URL到显示页面，中间都经历了什么（尽可能写详细，最好回答出TCP的三次握手和四次挥手，以及浏览器加载页面的细节）
    （https://blog.csdn.net/weixin_40260594/article/details/79477675）
3. 说出你所熟知的HTTP状态码！GET和POST有啥区别！
     2** 成功      200
     3** 重定向    301 302 304
     4** 客户端错误  404 路径地址错误
     5** 服务器端错误  500 服务器遇到错误，无法完成请求   503超载或停机维护
    GET 请求可被缓存
    GET 安全性较差
    GET 请求保留在浏览器历史记录中
    GET 请求可被收藏为书签
    GET 请求不应在处理敏感数据时使用
    GET 请求有长度限制，URL的最大长度是2048个字符
    GET 数据在 URL 中对所有人都是可见的。

    POST 请求不会被缓存
    POST POST 比 GET 更安全，因为参数不会被保存在浏览器历史或web服务器日志中
    POST 请求不会保留在浏览器历史记录中
    POST 不能被收藏为书签
    POST 请求对数据长度没有要求
    POST 数据不会显示在 URL 中。

4. 什么是HTTP报文，你熟知的报文都有哪些！

5. 能说下304具体怎样实现吗？
    node实现可缓存的服务

    var http = require("http")
    var fs   = require("fs")
    var url  = require("url")

    http.createServer(function(req,res){
        var pathname = url.parse(req.url).pathname
        var fsPath = __dirname + pathname
        fs.access(fsPath, fs.constants.R_OK, function(err){ //fs.constants.R_OK - path 文件可被调用进程读取
            if(err) {
              console.log(err) //可返回404，在此简略代码不再演示
            }else {
              var file = fs.statSync(fsPath) //文件信息
              var lastModified = file.mtime.toUTCString()
              var ifModifiedSince = req.headers['if-modified-since']
              //传回Last-Modified后，再请求服务器会携带if-modified-since值来和服务器中的Last-Modified比较
              var maxAgeTime = 3 //设置超时时间
              if(ifModifiedSince && lastModified == ifModifiedSince) { //客户端修改时间和服务端修改时间对比
                  res.writeHead(304,"Not Modified")
                  res.end()
              } else {
                fs.readFile(fsPath, function(err,file){
                    if(err) {
                      console.log('readFileError:', err)
                    }else {
                        res.writeHead(200,{
                            "Cache-Control": 'max-age=' + maxAgeTime,
                            "Last-Modified" : lastModified
                        })
                        res.end(file)
                    }
                })
              }
            }
        })
    }).listen(3030)
6. 跨域是什么？http协议中如何判断跨域？如何解决跨域问题？
    跨域，指的是浏览器不能执行其他网站的脚本。它是由浏览器的同源策略造成的，是浏览器施加的安全限制。
    同源策略：协议，域名，端口号，一个不同，就是不同源。
    JSONP：JSONP只支持GET请求，不支持POST请求。
    CORS：服务器设置Access-Control-Allow-OriginHTTP响应头
    代理：后台处理
    document.domain+iframe 只有在主域名相同的情况下使用
    动态创建script标签        script标签不受同源策略影响

7. HTTP2具体内容？SDPY了解么？
    HTTP2新特性：
    二进制分帧
    首部压缩
    流量控制
    多路复用
    请求优先级
    服务器推送
    SPDY是Google开发的基于传输控制协议(TCP)的应用层协议 。Google最早是在Chromium中提出的SPDY协议。目前已经被用于Google Chrome浏览器中来访问Google的      SSL加密服务。
8. HTTPS如何实现？tsl/ssl是什么（https://blog.csdn.net/anningzhu/article/details/77517432）？对称加密、非对称加密在什么时候、对什么数据加密？
  网站要实现HTTPS访问，首选你需要申请一张SSL证书，然后将SSL证书部署到服务器端，开启443端口，就可以实现HTTPS访问了。另外，如何获得SSL证书呢？可以到CA机构申请付费和免费的SSL证书，目前一些机构推出了免费SSL证书，如沃通CA推出了3年期多域名免费SSL，可以进行免费申请。如何部署SSL证书了，在申请的时候，有相应的部署指导手册。
  SSL：（Secure Socket Layer，安全套接字层），位于可靠的面向连接的网络层协议和应用层协议之间的一种协议层。SSL通过互相认证、使用数字签名确保完整性、使用加密确保私密性，以实现客户端和服务器之间的安全通讯。该协议由两层组成：SSL记录协议和SSL握手协议。
  TLS：(Transport Layer Security，传输层安全协议)，用于两个应用程序之间提供保密性和数据完整性。该协议由两层组成：TLS记录协议和TLS握手协议。
  对称加密、非对称加密在什么时候、对什么数据加密？（https://blog.csdn.net/claram/article/details/78230583?locationNum=6&fps=1）
  （1） 对称加密加密与解密使用的是同样的密钥，所以速度快，但由于需要将密钥在网络传输，所以安全性不高。
  （2） 非对称加密使用了一对密钥，公钥与私钥，所以安全性高，但加密与解密速度慢。
  （3） 解决的办法是将对称加密的密钥使用非对称加密的公钥进行加密，然后发送出去，接收方使用私钥进行解密得到对称加密的密钥，然后双方可以使用对称加密来进行沟通。
9. DNS劫持是什么？
    DNS劫持又称域名劫持，是指在劫持的网络范围内拦截域名解析的请求，分析请求的域名，把审查范围以外的请求放行，否则返回假的IP地址或者什么都不做使请求失去响    应，其效果就是对特定的网络不能访问或访问的是假网址。
10. 封装一个AJAX库！