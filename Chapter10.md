### DOM
（文档对象模型）是针对HTML 和XML 文档的一个API（应用程序编程接口）

#### 节点层次（分四种 node document）

所有页面标记则表现为一个以特定节点为根节点的树形结构，文档节点是每个文档的根节点（eg html）

> 1 node类型 

1. DOM1级定义了一个node接口
* nodeName 和nodeValue属性，在使用这两个值以前，最好先检测一下节点的类型（利用if(someNode.nodeType==1){使用}）
* 节点关系 子父同胞 childNodes属性（内部所有节点都是同胞节点，他们的parentNode都都指向同一个节点）保存着一个NodeList是一种类数组对象，用于保存一组有序的节点可以通过位置来访问这些节点
  1.对arguments 对象使用Array.prototype.slice()方法可以将其转换为数组，也可以将NodeList 对象转换为数组具体方法分为： 
  2. 方法var arrayOfNodes = Array.prototype.slice.call(someNode.childNodes,0);
  3. E8及更早的版本将NodeList实现为一个COM对象，将其转化为数组必须手动枚举所有成员，可以使用怪癖检测方式
      function convertToArray(nodes){
          var array = null;
          try {
              array = Array.prototype.slice.call(nodes, 0); //针对非IE 浏览器
          } catch (ex) {
              array = new Array();
              for (var i=0, len=nodes.length; i < len; i++){
                array.push(nodes[i]);
              }
          }
          return array;
       }
  4. parentNode 该属性指向文档树中的父节点，包含在childNodes列表中的每个节点相互之间都是同胞节点可以使用previousSibling和nextSibling第一个和最后一个分别为null
  5. firstChild 和lastChild
  
* 操作节点
 1. appendChild()，用于向childNodes 列表的末尾添加一个节点 
 2. insertBefore()方法，接受两个参数：要插入的节点和作为参照的节点
 3. replaceChild()方法接受的两个参数是：要插入的节点和要替换的节点
* 其他方法
 1. cloneNode()，用于创建调用这个方法的节点的一个完全相同的副本 cloneNode()方法接受一个布尔值参数，表示是否执行深复制 在参数为true的情况下，执行深复制，也就是复制节点及其整个子节点树，（不会复制时间处理程序，但是在IE中存在bug，会复制事件处理程序，故在复制之前需要先移除事件处理程序）
 
> document类型

1. 文档子节点Document节点的子节点可以是DocumentType、Element、ProcessingInstruction或Comment (document.doctype)
 * 一般一个页面文档中只包含一个子节点，即<html>元素（注释时一定注意）。可以通过documentElement 或childNodes 列表来访问这个元素
 * document.body属性直接执行<body>元素
2. 文档信息 如document.title document.URL（地址栏中显示的URL） document.domain(页面的域名,可设置，值相同时可访问) document.referrer(链接到当前页面的那个页面的URL)
3. 查找元素 
  * document.getElementById()注意第一个方法在IE中若存在（<input><textarea><button><select>的name属性和id值相同，并且位于指定id元素的前面将会被返回）
  * document.getElementsByTagName()会返回一个HTMLCollection 对象 该对象除了索引外还提供按名称访问，可以通过name取得集合中的项namedItem()；getElementsByTagName()传入*正常包含整个页面的元素，但在IE中将commemt视为element，注释节点也会被返回
  * getElementsByName()最常使用getElementsByName()方法的情况是取得单选按钮，返回一个HTMLCollectioin。但是，对于这里的单选按钮来说，namedItem()方法则只会取得第一项（因为每一项的name 特性都相同

4. 特殊集合 除了属性和方法，document 对象还有一些特殊的集合，这些集合都是HTMLCollection 对象
* document.anchors 包含文档中所有带name 特性的<a>元素
* document.forms 包含文档中所有的<form>元素
* document.images，包含文档中所有的<img>元素
* document.links，包含文档中所有带href 特性的<a>元素

5. DOM一致性检测
由于DOM 分为多个级别，也包含多个部分，因此检测浏览器实现了DOM的哪些部分就十分必要，document.implementation 属性就是为此提供相应信息和功能的对象
* DOM1 级只为document.implementation 规定了一个方法，即hasFeature()接受两个参数：要检测的DOM功能的名称及版本号，返回true、false eg var hasXmlDom = document.implementation.hasFeature("XML", "1.0");

6. 文档写入
* write()接收一个字符串参数，文档加载结束后调用document.write()方法会重写整个页面（不管页面之前有什么内容将被替换）
* writeln()同上，带换行
* open()
* close()

> element类型

Element 类型用于表现XML或HTML元素，提供了对元素标签名、子节点及特性的访问

1. html元素。HTMLElement 类型直接继承自Element 并添加了一些属性。如id title lang dir className
2. 取得特性 getAttribute()removeAttribute()，开发人员经常不使用getAttribute()，而是只使用对象的属性（元素.属性）。只有在取得自定义特性值的情况下，才会使用getAttribute()方法。
3. 设置特性setAttribute()或者直接赋值div.id = "someOtherId";div.setAttribute("id", "someOtherId");
4. attributes 属性Element类型是使用attributes 属性的唯一一个DOM 节点类型。attributes 属性中包含一个NamedNodeMap，与NodeList 类似，也是一个“动态”的集合，NamedNodeMap 对象拥有下列方法
* getNamedItem(name)
* emoveNamedItem(name)
* setNamedItem(node)node)：向列表中添加节点，以节点的nodeName 属性为索引；
* item(pos)pos)：返回位于数字pos 位置处的节点
5. 创建元素document.createElement()
6 元素的子节点childNodes 属性中包含了它的所有子节点，这些子节点有可能是元素、文本节点、注释或处理指令

> text类型

1. 文本节点由Text 类型表示，nodeValue 属性或data 属性访问Text 节点中包含的文本可以通过下面方法进行操作
* appendData(text)将text添加至节点的末尾
* deleteData(offset,count)从指定位置删除指定字符
* insertData(offset, text)
* replaceData(offset, count, text)：
* splitText(offset)：从offset 指定的位置将当前文本节点分成两个文本节点。
* substringData(offset, count)
* length 属性保存着节点中字符的数目
2. document.createTextNode(‘text’)创建新文本节点
3. 规范化文本节点,这个方法是由Node 类型定义的（因而在所有节点类型中都存在），名叫normalize();element.normalize();
4. 分割文本节点提供了一个作用与normalize()相反的方法：splitText()
 
> comment类型 










