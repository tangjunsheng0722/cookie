# Cookie+Session  Cookie+Web Storage
## Cookie+Session概念
> 浏览器的缓存机制提供了可以将用户数据存储在客户端上的方式，可以利用cookie,session等跟服务端进行数据交互。

> cookie和session都是用来跟踪浏览器用户身份的会话方式
## 区别:
> 1.保存状态: cookie是保存在浏览器端的,session是保存在服务器端的

> 2.使用方式:
```
cookie机制：如果不是在浏览器中设置过期时间,cookie被保存在内存中,生命周期随浏览器关闭而结束;如果在浏览器中设置了过期时间,cookie被保存在硬盘,关闭浏览器cookie数据仍然存在,知道过期才消失.
            Cookie是服务器发给客户端的特殊信息，cookie是以文本的方式保存在客户端，每次请求时都带上它
session机制: 当服务器收到请求需要创建session对象时,首先检查客户端请求中是否包含session id;如果有服务器根据相应的session id返回session对象;如果没有,服务器会创建
新的session对象,并把session id在本次响应中通过cookie的方式返回给客户端,在交互中浏览器按照规则将sessionid发送给服务器。cookie禁用时使用url重写.
```
> 3.存储内容和大小
```
cookie: 以文本的方式保存字符串类型; 单个cookie保存的数据不超过4kb
session: 通过类似与Hashtable的数据结构来保存，能支持任何类型的对象(session中可含有多个对象);大小没有限制
```
> 4.安全性
```
cookie：针对cookie所存在的攻击：Cookie欺骗，Cookie截获; session的安全性大于cookie。
原因:  sessionID存储在cookie中，若要攻破session首先要攻破cookie
       sessionID是要有人登录，或者启动session_start才会有，所以攻破cookie也不一定能得到sessionID
       sessionID是加密的
```
## Web Storage
> WebStorage的目的是克服由cookie所带来的一些限制，当数据需要被严格控制在客户端时，不需要持续的将数据发回服务器。
```
1.提供一种cookie 之外的存储会话数据的路径
2.提供一种存储大量可以跨会话存在的数据机制
```
## 提供了两种会话机制 localStorage + sessionStorage
> localStorage + sessionStorage特征
```
1.生命周期
localStorage: localStorage的生命周期是永久的,除非主动删除数据,关闭浏览器和页面数据不会消失
sessionStorage: 引入了一个"浏览器窗口"概念,sessionStorage是在同源的窗口中始终存在的数据。只要这个浏览器窗口没有关闭，即使刷新页面或者进入同源另一个页面，数据依然存在。但是sessionStorage在关闭了浏览器窗口后就会被销毁。同时独立的打开同一个窗口同一个页面，sessionStorage也是不一样的。
2.存储大小: 大小限制一般都是 5MB
3.存储位置: 都保存在客户端,不与3服务器进行交互通信
4.存储类型: 只能存储字符串,复杂对象用JSON对象的stringify和parse来处理
5.获取方式: window.localStorage   window.sessionStorage
6.应用场景:
localStorage: 常用于长期登陆(+判断用户是否登陆),适合长期保存在本地的数据
sessionStorage: 敏感账号一次登陆
```
## webStorage的优点
```
1.存储空间大:cookie为4KB  webStorage为5MB
2.节省网络流量: webStorage不会传送到服务器,直接在本地获取,减少了客户端和服务器端的交互
3.快速获取: 不需要向服务器发送请求,直接在本地获取,所以速度快
4.安全性: WebStorage不会随着HTTP header发送到服务器端，所以安全性相对于cookie来说比较高一些，不会担心截获，但是仍然存在伪造问题
5.自定义一些方法,数据操作更方便:
    setItem (key, value) ——  保存数据，以键值对的方式储存信息。
    getItem (key) ——  获取数据，将键值传入，即可获取到对应的value值。
    removeItem (key) ——  删除单个数据，根据键值移除对应的信息。
    clear () ——  删除所有的数据
    key (index) —— 获取某个索引的key
6.提供会话级存储 sessionStorage
```