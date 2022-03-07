---
title: pdd一面
date: 2022-03-06 14:59:26
tags:
---
#### 回顾一下pdd一面
<!-- more -->

1、开始是简单的自我介绍

2、接下来是问了一个布局居中问题，哪些方式

答：flex，margin的auto，line-height，text-align:center

下来查了一下还有使用表格的方法，vertical-align: middle；display: table-cell；绝对定位：使用浮动；font-size

3、简单的编程题，leetcode中的版本号问题，但是最后结果有两个是不对的，下来又重新优化了一下，使用遍历即可解决，回想一下使用白板不能进行快速调试console.log，定位问题没定位出来。

> 给你两个版本号 version1 和 version2 ，请你比较它们。
>
> 版本号由一个或多个修订号组成，各修订号由一个 '.' 连接。每个修订号由 多位数字 组成，可能包含 前导零 。每个版本号至少包含一个字符。修订号从左到右编号，下标从 0 开始，最左边的修订号下标为 0 ，下一个修订号下标为 1 ，以此类推。例如，2.5.33 和 0.1 都是有效的版本号。
>
> 比较版本号时，请按从左到右的顺序依次比较它们的修订号。比较修订号时，只需比较 忽略任何前导零后的整数值 。也就是说，修订号 1 和修订号 001 相等 。如果版本号没有指定某个下标处的修订号，则该修订号视为 0 。例如，版本 1.0 小于版本 1.1 ，因为它们下标为 0 的修订号相同，而下标为 1 的修订号分别为 0 和 1 ，0 < 1 。
>
> 返回规则如下：
>
> 如果 version1 > version2 返回 1，
> 如果 version1 < version2 返回 -1，
> 除此之外返回 0。

```js
/**
 * @param {string} version1
 * @param {string} version2
 * @return {number}
 */
var compareVersion = function(version1, version2) {
  const v1 = version1.split('.')
  const v2 = version2.split('.')
  const maxNum = Math.max(v1.length, v2.length)
  let arr = []
  for (let i = 0; i < maxNum; i++) {
    const num = Number(v1[i] ? v1[i] : 0) - Number(v2[i] ? v2[i] : 0)
    console.log(num)
    arr.push(num)
  }
  console.log(arr)
  let returnNum = null
  for (let ii = 0; ii < maxNum; ii++) {
    if (arr[ii] > 0) {
      returnNum = 1
      break
    } else if (arr[ii] == 0) {
      returnNum = 0
    } else if (arr[ii] < 0) {
      returnNum = -1
      break
    }
  }
  return returnNum
};
```

这是下来自己重新写的一个，当时有最后比较arr的时候，使用了层层嵌套的if，处理不好

官方解法：

```js
var compareVersion = function(version1, version2) {
    const v1 = version1.split('.');
    const v2 = version2.split('.');
    for (let i = 0; i < v1.length || i < v2.length; ++i) {
        let x = 0, y = 0;
        if (i < v1.length) {
            x = parseInt(v1[i]);
        }
        if (i < v2.length) {
            y = parseInt(v2[i]);
        }
        if (x > y) {
            return 1;
        }
        if (x < y) {
            return -1;
        }
    }
    return 0;
};
```

方法二：双指针处理

```js
var compareVersion = function(version1, version2) {
    const n = version1.length, m = version2.length;
    let i = 0, j = 0;
    while (i < n || j < m) {
        let x = 0;
        for (; i < n && version1[i] !== '.'; ++i) {
            x = x * 10 + version1[i].charCodeAt() - '0'.charCodeAt();
        }
        ++i; // 跳过点号
        let y = 0;
        for (; j < m && version2.charAt(j) !== '.'; ++j) {
            y = y * 10 + version2[j].charCodeAt() - '0'.charCodeAt();
        }
        ++j; // 跳过点号
        if (x !== y) {
            return x > y ? 1 : -1;
        }
    }
    return 0;
};
```

4、接下来就是问了点简单地了一下项目，问到登录怎么做，怎么实现定位元素移动，旋转

5、最后问你还有什么想问的，就结束了今天的面试。
