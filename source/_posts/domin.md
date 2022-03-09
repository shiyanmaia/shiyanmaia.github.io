---
title: document.domain
date: 2022-01-25 13:27:58
---
谷歌将禁止修改docment.domain来解决跨域问题
https://developer.mozilla.org/zh-CN/docs/Web/API/Document/domain#setter

比如网站XXX.HHHH.COM和SSS.HHHH.COM不能通讯，但是可以设置上述的属性为公共域，便可访问。

看到个解决方案为使用 **Origin-Agent-Cluste**这一属性

Origin-Agent-Cluste: ?0

允许页面请求被源（而不是站点）隔离。如果设置为 true ( **Origin-Agent-Cluster: ?1** )，则要求浏览器按来源隔离页面。如果为假，则按站点

或者使用postMessage()或Channel Messaging API()代替document.domain

```js
主页面：https://a.hhhh.com

// 给 https://b.hhhh.com 发消息
iframe.postMessage('哈喽', 'https://b.hhhh.com');

// 接收信息
iframe.addEventListener('message', (event) => {
  // 把不想要的信息过滤掉
  if (event.origin !== 'https://b.hhhh.com') return;

  if (event.data === 'succeeded') {
    // 干点别的 ...
  }
});
iframe 页面：https://b.hhhh.com

// 接收信息
window.addEventListener('message', (event) => {
  // 拒绝其他信息
  if (event.origin !== 'https://a.hhhh.com') return;
  
  // 恢复消息
  event.source.postMessage('succeeded', event.origin);
});
```

