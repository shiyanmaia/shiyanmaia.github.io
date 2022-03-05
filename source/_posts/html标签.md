---
title: 处理用户输入html标签等
date: 2022-01-19 17:48:58
---
```js
a.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;').replace(/'/g, '&apos;')
```

```js
formatSpace (s) {
  return (s || '').split('').map(i => {
    if (i.charCodeAt(0) === 160) {
      return String.fromCharCode(32)
    }
    return i
  }).join('')
},
```
