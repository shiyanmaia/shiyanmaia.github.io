---
title: js小技巧
date: 2021-07-19 14:24:42
---

1、求和，最小值合最大值

利用 `reduce` 方法快速找到基本的运算。

`const array  = [5,4,7,8,9,2];`

求和：

`array.reduce((a,b) => a+b); // 输出35`

最大值：

`array.reduce((a,b) => a>b?a:b); // 输出9`

相反就是最小值

2、排序字符串，数字或对象等数组

字符串数组排序：

```js
const stringArr = ["Joe", "kapill", "Steve", "Musk"]
stringArr.sort();
// 输出 ["Joe", "Kapil", "Musk", "Steve"]

stringArr.reverse();
// 输出 ["Steve", "Musk", "Kapil", "Joe"]
```



数字数组排序：

```js
const array = [40, 100, 1, 5, 25, 10];
array.sort((a,b) => a-b);
// 输出 [1, 5, 10, 25, 40, 100]

array.sort((a,b) => b-a);
// 输出 [100, 40, 25, 10, 5, 1]
```



对象数组排序：

```js
const objectArr = [ 
    { first_name: 'Lazslo', last_name: 'Jamf' }, 
    { first_name: 'Pig', last_name: 'Bodine' }, 
    { first_name: 'Pirate', last_name: 'Prentice' } 
];
objectArr.sort((a,b) => a.last_name.localeCompare(b.last_name));
// 输出 
// (3) [{…}, {…}, {…}] 
// 0: {first_name: "Pig", last_name: "Bodine"} 
// 1: {first_name: "Lazslo", last_name: "Jamf"} 
// 2: {first_name: "Pirate", last_name: "Prentice"} 
// length: 3
```

3、从数组中过滤掉虚值

像 `0`、`undefined`、`null`、`false`、`""`、`''` 这样的假值可以通过下面的技巧轻易地过滤掉。

```js
const array = [3, 0, 6, 7, '', false];
array.filter(Boolean);

// 输出
(3) [3, 6, 7]
```

4、使用逻辑运算符处理需要条件判断的情况

```js
function doSomething(arg1){
    arg1 = arg1 || 10;
    // 如果arg1没有值，则取默认值 10
}

let foo = 10;
foo === 10 && doSomething();
// 如果 foo 等于 10, 则执行 doSomething();
// 输出：10

foo === 5 || doSomething();
// is the same thing as if (foo != 5) then doSomething(); 
// Output: 10
```

5、去除重复值

```js
const array = [5,4,7,8,9,2,7,5];
array.filter((item,idx,arr) => arr.indexOf(item) === idx);

// or

const better = [...new Set(array)];
// Output: [5, 4, 7, 8, 9, 2];
```

6、创建一个计数器对象或 Map

```js
let string = 'kapilalipak';

const table = {};
for(let char of string) {
    table[char] = table [char]+1 || 1;
}
// 输出 {k: 2, a: 3, p: 2, i: 2, l: 2}
```

or

```js
const countMap = new Map();
  for (let i = 0; i < string.length; i++) {
    if (countMap.has(string[i])) {
      countMap.set(string[i], countMap.get(string[i]) + 1);
    } else {
      countMap.set(string[i], 1);
    }
  }
// 输出
Map(5) {"k" => 2, "a" => 3, "p" => 2, "i" => 2, "l" => 2}
```

7、三元运算符

```js
function Fever(temp) {
    return temp > 97 ? 'Visit Doctor!'
      : temp < 97 ? 'Go Out and Play!!'
      : temp === 97 ? 'Take Some Rest!': 'Go Out and Play!';;
}

// 输出
Fever(97): "Take Some Rest!" 
Fever(100): "Visit Doctor!"
```

可以连续使用三元运算符

8、合并两个对象

```js
const user = { 
 name: 'Kapil Raghuwanshi', 
 gender: 'Male' 
 };
const college = { 
 primary: 'Mani Primary School', 
 secondary: 'Lass Secondary School' 
 };
const skills = { 
 programming: 'Extreme', 
 swimming: 'Average', 
 sleeping: 'Pro' 
 };

const summary = {...user, ...college, ...skills};
```

9、洗牌一个数组

利用内置的 `Math.random()` 方法。

```js
const list = [1, 2, 3, 4, 5, 6, 7, 8, 9];
list.sort(() => {
    return Math.random() - 0.5;
});
// 输出
(9) [2, 5, 1, 6, 9, 8, 4, 3, 7]
// 输出
(9) [4, 1, 7, 5, 3, 8, 2, 9, 6]
```

10、将十进制转换为二进制或十六进制

```js
const num = 10;

num.toString(2);
// 输出: "1010"
num.toString(16);
// 输出: "a"
num.toString(8);
// 输出: "12"
```

11、使用解构交换两个数

```js
let a = 5;
let b = 8;
[a,b] = [b,a]

[a,b]
// 输出
(2) [8, 5]
```

12、单行的回文数检查

`function checkPalindrome(str) {
  return str == str.split('').reverse().join('');
}
checkPalindrome('naman');
// 输出: true`