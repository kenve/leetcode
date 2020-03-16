## LeetCode 剑指 Offer (第 2 版) 题集解析

[LeetCode 剑指 Offer（第 2 版）题集](https://leetcode-cn.com/problemset/lcof/)

## 索引

- [面试题 58 - II 左旋转字符串](#面试题-58---II-左旋转字符串)

### [面试题 58 - II 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

> 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字 2，该函数将返回左旋转两位得到的结果"cdefgab"。

__解析 1：__ 字符串 [slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice) 方法提取字符串的一部分，并将其作为新字符串返回，而无需修改原始字符串。

`str.slice(beginIndex[, endIndex])` 方法接收两个参数，若两个参数都不传返回原字符串。

- `beginIndex` 索引值从零开始，提取次索引后的字符串。
  - 如果为负数则值为 `str.length + beginIndex`。(如：`beginIndex` 为 `-3` 会处理为 `str.length - 3`)。
  - 如果 `beginIndex` 的值大于或等于 `str.length`, `slice()` 返回空字符串。
- `endIndex` 可选参数。提取在此索引之前的字符串。该索引处的字符将不包括在内。
  - 如果 `endIndex` 省略，则 `slice()` 提取到字符串的末尾。
  - 如果为负数则值为 `str.length + endIndex`。(如：`endIndex` 为 `-3` 会处理为 `str.length - 3`)

```js
/**
 * @param {string} s
 * @param {number} n
 * @return {string}
 */
var reverseLeftWords = function(s, n) {
  return s.slice(n) + s.slice(0, n);
};
```

__解析 2：__ 字符串 [substring()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substring) 方法返回 start 和 end 索引之间或字符串末尾的指定部分的新字符串。

> **tips:** `substr()` 可能被废弃，避免使用，用 `substring()` 替代。

`str.substring(indexStart[, indexEnd])` 方法接收两个参数，若两个参数都不传返回原字符串。

- `indexStart` 要包含在返回的子字符串中的第一个字符的索引。
- `indexEnd` 可选参数。从返回的子字符串中排除的第一个字符的索引。

```js
/**
 * @param {string} s
 * @param {number} n
 * @return {string}
 */
var reverseLeftWords = function(s, n) {
  return s.substring(n) + s.substring(0, n);
};
```
