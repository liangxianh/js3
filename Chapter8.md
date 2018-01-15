### BOM

bom提供了很多对象，用于访问浏览器的功能，W3C 为了把浏览器中JavaScript 最基本的部分标准化，已经将BOM的主要方面纳入了HTML5 的规范

#### window
> 1.window

1. BOM 的核心对象是window，它表示浏览器的一个实例。它既是通过JavaScript 访问浏览器窗口的一个接口，又是ECMAScript 规定的Global 对象
2. 在全局环境中定义的方法和属性，都会成为window的方法和属性，但是不能直接用delete删除，而直接在window上定义的属性可以用delete删除，
   使用var 语句添加的window 属性有一个名为[[Configurable]]的特性，这个特性的值被设置为false，因此这样定义的属性不可以通过delete 操作符删除

> 2. 窗口关系和框架

1. 页面中包含框架，则每个框架都拥有自己的window 对象，并且保存在frames 集合中。可以通过window.frames[0]或者window.frames["name"]来引用对应的框架
2. 位置和大小
* 位置：screenLeft和screenTop （IE、Safari、Opera 和Chrome）；
        screenX和screenY（firefox）；
        可以使用 var leftPos = (typeof window.screenLeft == 'number')?window.screenLeft:window.screenX来兼容
* 准确的移动到新位置：moveTo()接收的是新位置的x 和y 坐标值，而moveBy()接收的是在水平和垂直方向上移动的像素数
* 大小：：innerWidth、innerHeight、outerWidth 和outerHeight（IE9+、Firefox、Safari、Opera 和Chrome）       
          
> 3. 导航和打开窗口
 
 1. window.open('要加载的URL','窗口目标（：_self、_parent、_top 或_blank）','一个特性字符串','表示新页面是否取代浏览器记录中当前加载页面的布尔值')
 如果给window.open()传递的第二个参数并不是一个已经存在的窗口或框架，那么该方法就会根据在第三个参数位置上传入的字符串创建一个新窗口或新标签页，如果没有传入第三个参数，那么就会
打开一个带有全部默认设置（工具栏、地址栏和状态栏等）的新浏览器窗口，调用close()方法还可以关闭新打开的窗口
2. 安全限制
3. 弹出窗口屏蔽程序

> 4. 间歇调用和超时调用

1. 前者是在指定的时间过后执行代码setInterval()，而后者则是每隔指定的时间就执行一次代码setTimeout()
2. 超时调用需要window 对象的setTimeout('字符串（就和在eval()函数中使用的字符串一样）或者函数','毫秒值')
3. 取消超时调用：clearTimeout(timeoutId)（clearInterval()），调用setTimeout()之后，该方法会返回一个数值ID，表示超时调用
4. 注意：超时调用的代码都是在全局作用域中执行的，因此函数中this 的值在非严格模式下指向window 对象，在严格模式下是undefined。


> 5. 系统对话框

1. 浏览器通过alert()、confirm()和prompt()、lert()方法可以调用系统对话框向用户显示消息

#### location

提供了与当前窗口中加载的文档有关的信息，还提供了一些导航功能，它既是window 对象的属性，也是document 对象的属性；
它将URL 解析为独立的片段

> 1. location对象的所有属性

1. hash 
2. host 如'www.wrox.com:80' 服务器名称和端口号（如果有）   
3. hostname 不带端口号的服务器名称
4. href 当前加载页面的完整的URL
5. pathname 返回URL的目录和（或）文件名
6. port URL指定的端口号（如8080）
7. protocol 返回页面使用的协议 （http）
8. search （如？key=value）返回URL的查询字符串，已问号开头

> 2. 查询字符串参数

1. 可以利用search属性，获取到所有的请求参数，用decodeURIComponent()分别解码name 和value（因为查询字符串应该是被编码过的

> 3.位置操作 

1. 改变浏览器位置的方法
* location.assign('URL')方法
* window.location = 'URL'
* location.href = 'URL'
二三方法与1方法效果相同，改变location对象的其他属性也会改变当前加载的页面（除hash外，其他都会以新的URL重新加载）
* location.replace('URL') ,以上的任何方式修改URL都可以回退，而想要禁用改功能，可以使用replace()方法
* location.reload([true])五true参数可能从缓存中加载数据，有true只能从服务器重新加载

#### navigator
现在已经成为识别客户端浏览器的事实标准

> 1. 对象属性

* appCodeName 浏览器名称，通常为Mozilla
* 。。。。。。。

> 2. 检测插件

* 对于非IE 可以使用plugins数组 navigator.plugins数组的每一项都包含 name description filename length（插件所处理的MIME类型数量）

> 3. 注册处理程序

* Firefox 2 为navigator 对象新增了registerContentHandler()和registerProtocolHandler()方法，可以让一个站点指明它可以处理特定类型的信息
* registerContentHandler(MIME类型，可处理该MIME类型的页面的URL，应用程序的名称)三个，第一个参数是RSS 源的MIME 类型。
* registerProtocolHandler()方法，它也接收三个参数：要处理的协议（例如，mailto 或ftp）、处理该协议的页面的URL 和应用程序的名称
* 是一种RSS基于XML标准，在互联网上被广泛采用的内容包装和投递协议。RSS(Really Simple Syndication)是一种描述和同步网站内容的格式，是使用最广泛的XML应用。


#### screen



#### history
该对象保存着上网的历史记录，

> 1. 常用方法和属性

* 可以使用history.go(-1（1,2,。）或者是一个字符串参数（跳转到包含该字符串的第一个位置，可能前进也可能后退） )
* history.back() history.forward()可以代替go()方法
* history.length属性








