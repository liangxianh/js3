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

> 1. 

> 2. 

> 3. 

> 4. 


#### nabigator screen history

> 1. 

> 2. 

> 3. 

> 4. 







