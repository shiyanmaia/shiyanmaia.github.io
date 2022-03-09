---
title: css三角，多行文本超出，滚动条相关
date: 2021-12-20 13:46:42
---

1、css三角形角标

```css
div {
  width: 0;
  height: 0;
  border: 5px solid transparent;
  border-top-color: red;
}
```

2、css一行文本超出

```css
overflow: hidden;
text-overflow:ellipsis;
white-space: nowrap;
```

3、多行文本超出显示

```
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```

4、修改滚动条样式

隐藏`div`元素的滚动条

```
div::-webkit-scrollbar {
    display: none;
    
}
复制代码
```

div::-webkit-scrollbar 滚动条整体部分

div::-webkit-scrollbar-thumb 滚动条里面的小方块，能向上向下移动（或往左往右移动，取决于是垂直滚动条还是水平滚动条）

div::-webkit-scrollbar-track 滚动条的轨道

div::-webkit-scrollbar-button 滚动条的轨道的两端按钮，允许通过点击微调小方块的位置。

div::-webkit-scrollbar-track-piece 内层轨道，滚动条中间部分

div::-webkit-scrollbar-corner 边角，即两个滚动条的交汇处

div::-webkit-resizer 两个滚动条的交汇处上用于通过拖动调整元素大小的小控件

注意此方案有兼容性问题，一般需要隐藏滚动条时我都是用一个色块通过定位盖上去，或者将子级元素调大，父级元素使用overflow-hidden截掉滚动条部分。

5、隐藏页面元素

display-none: 元素不会占用空间，在页面中不显示，子元素也不会显示。

opacity-0: 元素透明度将为`0`，但元素仍然存在，绑定的事件仍旧有效仍可触发执行。

visibility-hidden：元素隐藏，但元素仍旧存在，占用空间，页面中无法触发该元素的事件。