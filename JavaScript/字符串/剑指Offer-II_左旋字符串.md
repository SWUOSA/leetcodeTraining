# 剑指Offer58-II.左旋转字符

## 一、题目

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**

```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```

**示例 2：**

```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

[力扣链接]: https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/

## 二、思路

### 1.思路一，不在字符串上修改

如果没有指出非要在原字符串上修改，那么本体较为简单。我只需要将不断地将尾部字符拼接到字符串的前部，拼接次数为length-n次（n为传入的数）

```javascript
  while (i < length - n) {
    s = s[length - 1] + s
    i++
  }
```

之后再使用slice截取函数原来了length长度即可。

```javascript
return s.slice(0, length)
```

### 2.思路二，在原字符串上操作

很明显，js中字符串并不适合我们直接操作。我们先将它转换为字符串。

```javascript
const strArr = Array.from(s)
```

我们会对它进行多次反转的操作。我们要实现具体到位数的反转，那自带的reverse函数肯定是不行的。

我们写一个reverse

```javascript
function reverWord(strArr, start, end) {
  let temp
  while(start < end) {
    temp = strArr[start]
    strArr[start] = strArr[end]
    strArr[end] = temp
    start++
    end--
  }
}
```

那么我们就可以通过先反转整体字符串，再反转前n个字符，然后再反转后n个字符即可。

```javascript
 reverseWords(strArr, 0, length - 1)
 reverseWords(strArr, 0, length - n - 1)
 reverseWords(strArr, length - n, length - 1)
```

最后返回式不要忘记转换为字符串

```javascript
return strArr.join('')
```

## 三、代码

### 1.思路1

```javascript
var reverseLeftWords = function(s, n) {
  const length = s.length;
  let i = 0;
  while (i < length - n) {
    s = s[length - 1] + s;
    i++;
  }
  return s.slice(0, length);
};
```

### 2.思路2

```javascript
/**
 * @param {string} s
 * @param {number} n
 * @return {string}
 */
var reverseLeftWords = function (s, n) {
    /** Utils */
    function reverseStrArr(strArr, start, end) {
        let temp;
        while (start < end) {
            temp = strArr[start];
            strArr[start] = strArr[end];
            strArr[end] = temp;
            start++;
            end--;
        }
    }
    let strArr = s.split('');
    let length = strArr.length;
    reverseStrArr(strArr, 0, length - 1);
    reverseStrArr(strArr, 0, length - n - 1);
    reverseStrArr(strArr, length - n, length - 1);
    return strArr.join('');
};
```

