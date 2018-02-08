### 第十一章 DOM扩展

> 选择符API

1. querySelector('css选择器') 返回匹配的第一个元素或null 
2. querySelectAll('选择器') 返回一个NodeList实例（未找到时为空），要访问其中的每个元素，可以使用item()方法 ListObj[i]或者ListObj.item(i)
3. matchesSelector('选择器') 返回true 或false 有兼容性


> 元素遍历

1. 由于IE9以及之前的版本不会返回文本节点，而其他浏览器都会返回文本节点是的childNodes和firstChild等属性行为不一致
* childElementCount：返回子元素（不包括文本节点和注释）的个数。
* firstElementChild：指向第一个子元素；firstChild 的元素版。
* lastElementChild：指向最后一个子元素；lastChild 的元素版。
* previousElementSibling：指向前一个同辈元素；previousSibling 的元素版。
* nextElementSibling：指向后一个同辈元素；nextSibling 的元素版。

> HTML5

1. 与类相关的扩充
* document(OR 具体的元素).getElementsByClassName('一个包含一或多个类名的字符串（同时含有）')方法  返回NodeList 
* classList属性,是新集合类型DOMTokenList 的实例,有length属性，可以使用item()或者方括号访问每个元素，还有如下方法如div.classList.remove("user");
  1. add(value)：将给定的字符串值添加到列表中。如果值已经存在，就不添加了。
  2. contains(value)：表示列表中是否存在给定的值，如果存在则返回true，否则返回false。
  3. remove(value)：从列表中删除给定的字符串。
  4. toggle(value)：如果列表中已经存在给定的值，删除它；如果列表中没有给定的值，添加它。

2. 焦点管理
* document.activeElement 属性，始终会引用DOM 中当前获得了焦点的元素
* document.hasFocus()方法，这个方法用于确定文档是否获得了焦点。

3. HTMLDocument的变化

* readyState属性 取值loading(正在加载文档)和complete(文档加载完成)
* 兼容模式 IE新增compatMode属性 浏览器采用哪种渲染模式（标准为CSS1Compat，混杂模式为BackCompat）该属性也作为h5的标准
* head属性 新增了document.head属性，引用文档的head元素（chrome和safari5实现了）

4. 字符集属性 document.charset   document.defaultCharset
5. 自定义数据属性 h5规定可以给元素添加非标准的属性，需加前缀data-，添加之后可以dataset属性来访问自定义属性的值
如<div id="myDiv" data-appId="12345" data-myname="Nicholas"></div>
  var div = document.getElementById("myDiv");
  //取得自定义属性的值
  var appId = div.dataset.appId;
  var myName = div.dataset.myname;
  div.dataset.appId = 23456;
  div.dataset.myname = "Michael";
6. 插入标记
  * innerHTML属性，写模式下，innerHTML 的值会被解析为DOM 子树
  * outerHTML属性，读模式下，返回调用他的元素及所有子节点的HTML标签；写模式下创建DOM子树，然后用这个DOM子树完全替换调用元素
  * insertAdjacentHTML('插入的位置beforebegin|afterbegin|beforeend|afterend','要插入的HTML文本')
  * 内存和性能问题

7. scrollIntoView()方法

> 专有扩展 



















