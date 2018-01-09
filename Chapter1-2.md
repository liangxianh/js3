## 第一章 js简介 
> 1.js为何而生,发展史

JS的出现是为了在在客户端进行一些基本的验证，而现在是一门功能全面的编程语言；
开发者 Netscape 公司的布兰登•艾奇与1995年创立liveScript后修改为javascript，在js1.1发布后微软就在其Internet Explorer 3 中加入了名为JScript 的JavaScript 实现，两者都不符合ecmaScript262标准，

> 2.JS包括三部分内容

  核心（ECMAScript）共有六版-2015年6月17日，ECMAScript 6发布正式版本，即ECMAScript 2015。（1234）
  文档对象模型（DOM）
  浏览器对象模型（BOM）
  
> 3.js宿主环境

常见的有web浏览器，node（服务器端脚本），adobe flash
  （Adobe Flash，用于设计和编辑Flash文档，以及Adobe Flash Player，用于播放Flash文档。）
  
> 4.ECMAscript兼容

  是指不同浏览器对ECMAscript的支持情况和标准么?开发新版本的js要符合的要求
  DOM（由w3c）为了控制浏览器互不兼容的情况（主要IE4和Netscape4之间）；
 （Document Object Model，文档对象模型，是HTML与XML的应用编程接口（API））
  
> 5.DOM级别

Web浏览器对DOM有不同程度的支持
1. 级由DOM核心与DOM HTML两个模块组成；
	  DOM核心:一些基本的CURD
	  DOMhtml: image,Table,Form,Input,Select...HTML标签对象化
2. 级DOM通过对象接口增加了对鼠标和用户界面事件（DHTML长期支持鼠标与用户界面事件）、范围、遍历（重复执行DOM文档）和层叠样式表（CSS）的支持。同时也对 DOM1的核心进行了扩展，从而可支持XML命名空间。2级DOM引进了几个新DOM模块来处理新的接口类型：
    DOM视图：描述跟踪一个文档的各种视图（使用CSS样式设计文档前后）的接口；
    DOM事件：描述事件接口；
    DOM样式：描述处理基于CSS样式的接口；
    DOM遍历与范围：描述遍历和操作文档树的接口；
3. 级DOM通过引入统一方式载入和保存文档和文档验证方法对DOM进行进一步扩展，DOM3包含一个名为“DOM载入与保存”的新模块，DOM核心扩展后可支持XML1.0的所有内容，包括XML Infoset、 XPath、和XML Base。
  
> 6. BOM(兼容较多)没有统一的标准

  主要功能：
  1. 弹出新浏览器窗口的能力；
  2. 移动、关闭和更改浏览器窗口大小的能力；
  3. 可提供WEB浏览器详细信息的导航对象；
  4. 可提供浏览器载入页面详细信息的本地对象；
  5. 可提供用户屏幕分辨率详细信息的屏幕对象；
  6. 支持Cookies；
  7. Internet Explorer对BOM进行扩展以包括ActiveX对象类，可以通过JavaScript来实现ActiveX对象。
有了HTML5，BOM 实现的细节有望朝着兼容性越来越高的方向发展

## 第二章js使用
> 1. 由<script>标签引入(html4.01规范)有六个属性
  
  1. async(异步,异步加载完成就执行)
	2. charset
	3. defer(异步,异步加载完成后等待所有元素解析完成之后，DOMContentLoaded 事件触发之前执行)
	4. language(不用了)
	5. src 指定的url可以是跨域的
	6. type
  
  附: defer和 async区别
1. <script src="script.js"></script>
    没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是在渲染该 script 标签之下的文档元素之前，也就是说不等待后续载入的文档元素，读到就加载并执行。
2. <script async src="script.js"></script>
    有 async，加载和渲染后续文档元素的过程将和 script.js 的加载与执行并行进行（异步）。
3. <script defer src="myscript.js"></script>
    有 defer，加载后续文档元素的过程将和 script.js 的加载并行进行（异步），但是 script.js 的执行要在所有元素解析完成之后，DOMContentLoaded 事件触发之前完成。
    
    
总结：

1. defer 和 async 在网络读取（下载）这块儿是一样的，都是异步的（相较于 HTML 解析）
2. 它俩的差别在于脚本下载完之后何时执行，显然 defer 是最接近我们对于应用脚本加载和执行的要求的
3. 关于 defer，此图未尽之处在于它是按照加载顺序执行脚本的，这一点要善加利用
4. async 则是一个乱序执行的主，反正对它来说脚本的加载和执行是紧紧挨着的，所以不管你声明的顺序如何，只要它加载完了就会立刻执行
5. 仔细想想，async 对于应用脚本的用处不大，因为它完全不考虑依赖（哪怕是最低级的顺序执行），不过它对于那些可以不依赖任何脚本或不被任何脚本依赖的脚本来说却是非常合适的，最典型的例子：Google Analytics

> 2 引入的位置和方式

 在html中位置头部,现在优选body之前内容之后,可以进行异步加载但是多个异步加载文件执行顺序不确定
但是在xhtml中使用时若有判断<,将作为新的标签来解析,故更加严格(两种方式避免 1使用符号实体&lt;2 使用CData片断)

> 3 优选外部js文件(可维护,可缓存,适应未来)

> 4 文档模式

  最初混杂和标准,后来准标准模式
  
  如何开启:
  1. 混杂:文档开始出没有类型声明
  2. 标准:
    <!-- HTML 4.01 严格型 -->
    <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
    <!-- XHTML 1.0 严格型 -->
    <!DOCTYPE html PUBLIC"-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    <!-- HTML 5 -->
    <!DOCTYPE html>
  3. 准标准:
    <!-- HTML 4.01 过渡型 -->
    <!DOCTYPE HTML PUBLIC"-//W3C//DTD HTML 4.01 Transitional//EN""http://www.w3.org/TR/html4/loose.dtd">
    <!-- HTML 4.01 框架集型 -->
    <!DOCTYPE HTML PUBLIC"-//W3C//DTD HTML 4.01 Frameset//EN""http://www.w3.org/TR/html4/frameset.dtd">
    <!-- XHTML 1.0 过渡型 -->
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
    <!-- XHTML 1.0 框架集型 -->
    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">

> 5 <noscript>标签
  
当浏览器不支持js标签或支持的脚本被禁用时 用改标签进行替换，内容可以包含在body中的任何元素 
