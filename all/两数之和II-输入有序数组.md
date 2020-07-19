### [167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

**题目：** 给定一个已按照 *升序排列*  的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1  必须小于  index2。

说明:

- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

示例:

```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```

**题解一：双指针**

```js
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (numbers, target) {
  let index1 = 0;
  let index2 = numbers.length - 1;
  while (index1 < index2) {
    let sum = numbers[index1] + numbers[index2];
    if (sum > target) {
      index2--;
    } else if (sum < target) {
      index1++;
    } else {
      return [index1 + 1, index2 + 1];
    }
  }
  return [-1, -1];
};
```

复杂度分析：

- 时间复杂度：O(n)，其中 n 是数组的长度。两个指针移动的总次数最多为 n 次。
- 空间复杂度：O(1)。

**题解二：二分查找**

在数组中找到两个数，使得它们的和等于目标值，可以首先固定第一个数，然后寻找第二个数，第二个数等于目标值减去第一个数的差。利用数组的有序性质，可以通过二分查找的方法寻找第二个数。为了避免重复寻找，在寻找第二个数时，只在第一个数的右侧寻找。

```js
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (numbers, target) {
  let len = numbers.length,
    left = 0,
    right = len - 1,
    mid = 0;
  for (let i = 0; i < len; ++i) {
    left = i + 1;
    while (left <= right) {
      mid = parseInt((right - left) / 2) + left;
      if (numbers[mid] == target - numbers[i]) {
        return [i + 1, mid + 1];
      } else if (numbers[mid] > target - numbers[i]) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    }
  }
  return [-1, -1];
};
```

复杂度分析：

- 时间复杂度：O(nlogn)，其中 n 是数组的长度。需要遍历数组一次确定第一个数，时间复杂度是 O(n)，寻找第二个数使用二分查找，时间复杂度是 O(logn)，因此总时间复杂度是 O(nlogn)。
- 空间复杂度：O(1)。
