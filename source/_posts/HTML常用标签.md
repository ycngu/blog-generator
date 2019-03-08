---
title: HTML常用标签
date: 2018-10-01 23:52:52
tags: [javascript]
---
# HTML常用标签
> * a
> * img
> * div / span
> * form
> * input / button
> * ol / ul / li
> * iframe
<!--more-->
## a
【标签】&lt;a&gt;&lt;/a&gt;
【属性】
href：链接地址（要跳转到的页面的地址）
target：目标，打开新网页的形式
取值：
     _blank：在新标签页中打开
     _self：在自身页面中打开（默认值）
title：鼠标放到链接上的提示

## img 
【标签】&lt;img&gt;	
【属性】
        src：图片地址（绝对/相对）
        width：图像宽度
        height：图像高度

## div /span
 【标签】&lt;div&gt;	&lt;/div&gt;	 &lt;span&gt;	&lt;/span&gt;	
  - div是 division的缩写,意思是**分隔**,span意思是**范围**
  - div的display为block，span的display为inline
  - div常用于页面布局，span用于划分行内段落
  

##  form / input / button
 form,表单最常见的就是注册和登陆表单，通常与input / button一起用
【标签】&lt;form&gt;	&lt;/form&gt;	
【常见属性】
        action：提交的服务器地址
        method：表单数据提交的方式，取值： get：明文提交/post：隐式提交
        name：定义表单名称，JS用到的比较多
        id： 独一无二的标识
如：&lt;form action="url" method="get/post"&gt;	 &lt;/form&gt;	

  【标签】&lt;input&gt;	
  【主要属性】
        type：根据不同的type属性值可以创建各种类型的输入字段
        value：最终提交给服务器的值
        name：控件的名称，提供给服务器使用，没有name，控件则无法提交
        id：唯一标识，只能在当前页面使用，服务器不能用
        disabled：禁用，不能被提交
 【注意】
    **input是空标签，button不是，空标签不能有子元素**

【标签】&lt;button&gt;	&lt;/button&gt;	
 【主要属性】
   type：规定按钮的类型，有button，submit，reset
   【注意】
   **当button位于form内部时，如果不标明type,type属性自动设置为submit**
   **当input的type为submit时，也可以提交表单**
##  hr
【标签】&lt;hr&gt;	
【属性】
        size：尺寸，取值单位为 px（像素），可以省略
        width：宽度，取值单位为px（像素）可以省略或百分比
        color：颜色，取值自然颜色值
        align：水平对齐方式，取值：left/center/right
##  ol ，ul , li
【标签】&lt;ol&gt;	&lt;/ol&gt;	 &lt;ul&gt;	&lt;/ul&gt;	 &lt;li&gt;	&lt;/li&gt;	
 - ol , Ordered List 有序列表
 - ul , Unordered List 无序列表
 -  li , List Item 列表项目

一般是列表包裹着列表项
如
```
<ol>
  <li></li>
  <li></li>
  <li></li>
</ol>

<ul>
  <li></li>
  <li></li>
  <li></li>
</ul>
```

## iframe

iframe是嵌入页面，现在已经很少使用了
【标签】&lt;iframe&gt;	&lt;/iframe&gt;	
【主要属性】
frameborder：规定是否显示框架周围的边框。
src：	规定在 iframe 中显示的文档的 URL。
height：规定 iframe 的高度。
width:规定 iframe 的宽度。
