# vue学习-指趣学院李南江视频资料

**lib里vue.js和vue-router.js,vuex.js

### 01.开篇 

### 	1.什么是Vue?

  Vue.js 是一套构建用户界面的`框架`，它不仅易于上手，还可以与其它第三方库整合(Swiper、IScroll、...)。
  2.框架和库的区别?
  框架：是一套完整的解决方案；对项目的`侵入性`较大，项目如果需要更换框架，则需要重构整个项目。
  库（插件）：提供某一个小功能，对项目的`侵入性`较小，如果某个库无法完成某些需求，可以很容易切换到其它库实现需求。
  例如: 从jQuery 切换到 Zepto, 无缝切换
        从IScroll切换到ScrollMagic, 只需要将用到IScroll的代码替换成ScrollMagic代码即可

###   	3.为什么要学习框架?

  提升开发效率：在企业中，时间就是效率，效率就是金钱；
  前端提高开发效率的发展历程：原生JS -> jQuery之类的类库 -> 前端模板引擎 ->  Vue / React / Angular

###   	4.框架有很多, 为什么要先学Vue

  Vue、Angular、React一起，被称之为前端三大主流框架！
  但是Angular、React是老外编写的, 所以所有的资料都是英文的
  而Vue是国人编写的, 所以所有的资料都是中文的, 并且Vue中整合了Angular、React中的众多优点
  所以为了降低我们的学习难度, 我们先学Vue, 学完之后再学习Angular和React

###   	5.使用Vue有哪些优势?

  	5.1Vue的核心概念之一:
      	通过数据驱动界面更新, 无需操作DOM来更新界面
      	使用Vue我们只需要关心如何获取数据, 如何处理数据, 如何编写业务逻辑代码,
      	我们只需要将处理好的数据交给Vue, Vue就会自动将数据渲染到模板中(界面上)
  	5.2Vue的核心概念之二:
      	组件化开发，我们可以将网页拆分成一个个独立的组件来编写
      	将来再通过封装好的组件拼接成一个完整的网页
     	 https://cn.vuejs.org/images/components.png

## 02-基本模板

### 	1.Vue框架使用方式

​    1.1传统下载导入使用
​    		1.2vue-cli安装导入使用

### 	2.Vue框架使用步骤

​    2.1下载Vue框架
​    		2.2导入Vue框架
​    		2.3创建Vue实例对象
​    		2.4指定Vue实例对象控制的区域
​    		2.5指定Vue实例对象控制区域的数据

```html
<head>
    <meta charset="UTF-8">
    <title>02-Vue基本模板</title>
	<!--1.下载后导入vue.js-->
    <script src="lib/vue.js"></script>
</head>
<body>
<div id="app">
    <p>{{ name }}</p>
</div>
<script>
    //2.创建Vue实例对象
    let vue = new Vue({
       //3.告诉Vue的实例对象，将来需要控制界面上的那个区域
        el: '#app',
        //4.告诉Vue实例对象，被控制区域的数据是什么
        data: {
            name: "李南江"
        }
    });
</script>
```

## 03-数据单向绑定

### 1.MVVM设计模式

在MVVM设计模式中由3个部分组成
		M : Model      数据模型(保存数据, 处理数据业务逻辑)
		V : View       视图(展示数据, 与用户交互)
		VM: View Model 数据模型和视图的桥梁(M是中国人, V是美国人, VM就是翻译)
		MVVM设计模式最大的特点就是支持数据的双向传递
		数据可以从 M -> VM -> V
		也可以从   V -> VM -> M

#### 2.Vue中MVVM的划分

### Vue其实是基于MVVM设计模式的

​		被控制的区域: View
​		Vue实例对象 : View Model
​		实例对象中的data: Model

### 3.Vue中数据的单向传递

我们把"数据"交给"Vue实例对象", "Vue实例对象"将数据交给"界面"
      Model --- ->  View Model   --- ->   View

## 04-数据双向传递

### 	1、Vue调试工具

​    -下载vuejs-devtools_v5.3.0.crx包
​    		-改扩展名为rar，然后解压缩；
​    		-谷歌浏览器安装：扩展程序---加载已解压的程序
​    		-重启浏览器完成安装。

### 	2.数据双向绑定

默认情况下Vue只支持数据单向传递 M -> VM -> V
但是由于Vue是基于MVVM设计模式的, 所以也提供了双向传递的能力
在<input>、<textarea> 及 <select> 元素上可以用 v-model 指令创建双向数据绑定
	注意点: v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值
	而总是将 Vue 实例的数据作为数据来源

## 05-常用指令v-once

### 	1.什么是指令?

​	指令就是Vue内部提供的一些自定义属性,
​			这些属性中封装好了Vue内部实现的一些功能
​			只要使用这些指令就可以使用Vue中实现的这些功能

### 	2.Vue数据绑定的特点

​	只要数据发生变化, 界面就会跟着变化

### 	3.v-once指令:

​	让界面不要跟着数据变化, 只渲染一次
​		只渲染元素和组件一次。随后的重新渲染，
​		元素/组件及其所有的子节点将被视为静态内容并跳过。
​		这可以用于优化更新性能。

例如：

```html
<div id="app">
    <p v-once="">原始数据：{{ name }}</p>
    <p>当前数据：{{ name }}</p>
</div>
<script>
    let vue = new Vue({
        el: '#app',
        data: {
            name: "程"
        }
    });
</script>
```

## 06-v-clock指令

### 1.Vue数据绑定过程

1.1会先将未绑定数据的界面展示给用户
		1.2然后再根据模型中的数据和控制的区域生成绑定数据之后的HTML代码
		1.3最后再将绑定数据之后的HTML渲染到界面上
		正是在最终的HTML被生成渲染之前会先显示模板内容
		所以如果用户网络比较慢或者网页性能比较差, 那么用户会看到模板内容

### 2.如何解决这个问题

利用v-cloak配合 [v-cloak] {display: none}默认先隐藏未渲染的界面
等到生成HTML渲染之后再重新显示

### 3.v-cloak指令作用:

数据渲染之后自动显示元素
这个指令保持在元素上直到关联实例结束编译。
和 CSS 规则如 [v-cloak] { display: none } 一起用时，
这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

例子：

```html
<div id="app">
    <p v-cloak>{{ name }}</p>
</div>
<script>
    let vue = new Vue({
        el: '#app',
        data: {
            name: "慢慢慢！！！"
        }
    });
</script>
```

