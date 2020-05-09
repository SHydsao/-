# clear-float
css
css浮动与清除浮动
浮动相关知识
什么是浮动？
​ 浮动元素会脱离文档流并向左/向右浮动，直到碰到父元素或者另一个浮动元素

浮动元素float属性的取值：
​ left: 元素向浮动

​ right: 元素向右浮动

​ none: 默认值，元素不浮动，并会显示在其在文本中出现的位置

浮动的特征
​

​ float属性应该是css世界最令人意外的属性了，倒不是因为他的表现，而是他的设计初衷竟然只是为了实现“文字环绕图片”的效果。只不过因为float属性的一些特性，才导致其被到处使用以致于产生了诸多不利于维护的页面。 下面看看float属性的特性：

包裹性：即此时元素width会像height一样由子元素决定，而不是默认撑满父元素。
块状化并格式化上下文：这个就是后面会讲的BFC特性。块状是指元素设置float: left之后，其display的计算值就成了block。格式化上下文是指会创建一个BFC，这个后面会讲。
没有任何margin合并；
脱离文档流：float设计的初衷就是为了“文字环绕”效果，为了让文字环绕图片，就需要具备两个条件。第一是元素高度坍塌，第二是行框盒子不可与浮动元素重叠。而元素高度坍塌就导致元素后面的非浮动块状元素会和其重叠，于是他就像脱离文档流了。
前三个特性都是正能量满满，但是最后一个特性却给我们开发者带来了很多麻烦，需要用到clear来清除浮动。

clear的作用和不足
大家都知道clear: both可以清除前面浮动元素的浮动，但实际上，他并不是真的清除了浮动。

clear的定义是：元素盒子的边不能与前面的浮动元素相邻。也就是虽然浮动元素高度坍塌，但是设置了clear: both的元素却将其高度视为仍然占据位置。

clear只能作用于块级元素，并且其并不能解决后面元素可能发生的文字环绕问题。

BFC清除浮动
BFC全称是块状格式化上下文，它是按照块级盒子布局的。我们了解他的特征、触发方式、常见使用场景这些就够了。

BFC的主要特征
✦ BFC容器是一个隔离的容器，和其他元素互不干扰；所以我们可以用触发两个元素的BFC来解决垂直边距折叠问题。 ✦ BFC可以包含浮动；通常用来解决浮动父元素高度坍塌的问题。

其中，BFC清除浮动就是用的“包含浮动”这条特性。 那么，怎样才能触发BFC呢？

BFC的触发方式
我们可以给父元素添加以下属性来触发BFC： ✦ float 为 left | right ✦ overflow 为 hidden | auto | scorll ✦ display 为 table-cell | table-caption | inline-block | flex | inline-flex ✦ position 为 absolute | fixed

所以我们可以给父元素设置overflow:auto来简单的实现BFC清除浮动，但是为了兼容IE最好用overflow:hidden。但是这样元素阴影或下拉菜单会被截断，比较局限。
