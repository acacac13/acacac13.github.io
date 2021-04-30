---
title: v-if与v-show的区别
date: 2021-04-28 13:59:04
tags: 
  - vue
  - 前端
  - 条件渲染
categories: 前端
---

# vue中v-if与v-show的区别

共同点：

​	v-if与v-show都能动态控制dom元素的显示隐藏

不同点：

​	查看vue的官方文档

![v-if vs v-show](https://gitee.com/acacac13/images/raw/master/20210428140527.png)

​	简单来说就是v-if显示隐藏是将dom元素整个添加或删除，而v-show隐藏则是为该元素添加css--display:none，dom元素还在。

​	v-show不支持 <template>元素，也不支持 v-else。

​	==注意：==当一个元素默认在css中加了display：none属性，这时通过v-show修改为true是无法让元素显示的。原因是显示隐藏切换，只是会修改**element style为display:""或者display:none,并不会覆盖掉或修改已存在的css属性。**

- **1.手段**：v-if是动态的向DOM树内添加或者删除DOM元素；v-show是通过设置DOM元素的display样式属性控制显隐；
- **2.编译过程**：v-if切换有一个局部编译/卸载的过程，切换过程中合适地销毁和重建内部的事件监听和子组件；v-show只是简单的基于css切换；
- **3.编译条件**：v-if是惰性的，如果初始条件为假，则什么也不做；只有在条件第一次变为真时才开始局部编译（编译被缓存？编译被缓存后，然后再切换的时候进行局部卸载); v-show是在任何条件下（首次条件是否为真）都被编译，然后被缓存，而且DOM元素保留；
- **4.性能消耗：**v-if有更高的切换消耗；v-show有更高的初始渲染消耗；
- **5.使用场景：**v-if适合运营条件不大可能改变；v-show适合频繁切换。

