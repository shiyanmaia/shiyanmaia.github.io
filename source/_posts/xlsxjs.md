---
title: xlsx.js的简单使用
date: 2022-03-08 17:48:58
tags:
---

```js
let workbook = XLSX.utils.book_new()
/*
        XXX| A | B | C | D | E | F | G |
        ---+---+---+---+---+---+---+---+
        1 | S | h | e | e | t | J | S |
        2 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
        3 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |

        XLSX.utils.aoa_to_sheet获取JS值数组的数组，
        并且返回一个工作表寻找输入数据。
        Numbers，Booleans和Strings都被存储为相应的样式。
        Date被存储为date或者是numbers。跳过数组孔和显式“未定义”值。
        null值可能被剔除。所有其它值存储为字符串。

        生成实例表：
        var ws = XLSX.utils.aoa_to_sheet([
            "SheetJS".split(""),
            [1,2,3,4,5,6,7],
            [2,3,4,5,6,7,8]
        ]);
      */
const pushData = []
// pushData.push([`Data Range:${this.xslxFilename}`])
// pushData.push(['#', 'Source', 'Target', 'Frequency'])
this.filteredViewItems.forEach((item, index) => {
  if (item.isSelected) {
    pushData.push([item.srcTerm || '', item.tgtTerm || '', item.frequency])
  }
})
let wb = XLSX.utils.aoa_to_sheet(pushData)
XLSX.utils.book_append_sheet(workbook, wb, 'Sheet1')
let wbout = XLSX.write(workbook, {
  bookType: 'xlsx',
  bookSST: true,
  type: 'array',
})
try {
  XLSX.writeFile(workbook, filename + '.xlsx')
} catch (e) {
  if (typeof console !== 'undefined') console.log(e, wbout)
}
return wbout

```

官方github：https://github.com/SheetJS/sheetjs