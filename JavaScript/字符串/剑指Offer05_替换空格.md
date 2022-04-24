# 剑指Offer05.替换空格

## 一、题目

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

[力扣原题]: https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/



## 二、思路

因为在js中，我们无法修改字符串，而本体很明显少不了对字符串的操作，所以我们先将字符串转为数组，一遍之后的操作。

```javascript
const strArr = Array.from(s)
```

对于将s替换成“%20”，我们很用利用方法直接对其进行删除插入替换。但是数组的数据结构使得这种算法复杂度较高。

所以本题我们采用其他方法。

我们可以先将需要返回的最终的字符串长度len算出，之后再利用双指针的方法。

```javascript
let count = 0
for (let i = 1; i < strArr.length-1; i++){
  if (strArr[i] === ' ') {
    count++
  }
}
len = strArr.length + count*2 -1
```

即left指针指向数组当前终点strArr.length-1，而right指向len，然后再利用将判断left所指字符，如果为“ ”，则从right写入“%20”，其他则正常写入，向左循环。

```javascript
let left = strArr.length -1, right = len
while (left >= 0) {
  if(strArr[left] === " ") {
    strArr[right--] = "0"
    strArr[right--] = "2"
    strArr[right--] = "%"
    left--
  } else {
    strArr[right--] = strArr[left--]
  }
}
```

最中返回时将数组转换为字符串即可。



## 三、完整代码

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
  const strArr = Array.from(s)
  let count = 0

  for(let i = 0; i < strArr.length; i++){
    if (strArr[i] === ' ') {
      count++
    }
  }

  let left = strArr.length - 1
  let right = strArr.length + count*2 - 1

  while (left >= 0) {
    if (strArr[left] == ' ') {
      strArr[right--] = '0'
      strArr[right--] = '2'
      strArr[right--] = '%'
      left--
    } else {
        strArr[right--] = strArr[left--]
    }
  }
  return strArr.join('')
};
```

