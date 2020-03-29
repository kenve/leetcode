### [面试题 57. 和为 s 的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

**题目：** 输入一个递增排序的数组和一个数字 s，在数组中查找两个数，使得它们的和正好是 s。如果有多对数字的和等于 s，则输出任意一对即可。

示例 1：

```
输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
```

示例 2：

```
输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
```

限制：

```
1 <= nums.length <= 10^5
1 <= nums[i] <= 10^6
```

**题解：**

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  // 增排序的数组首尾相加
  // 如果大于目标值尾部下标减 1
  // 如小于头部加 1
  // 刚好等于返回
  let left = 0;
  let right = nums.length - 1;
  while (left < right) {
    let sum = nums[left] + nums[right];
    if (sum > target) {
      right -= 1;
    } else if (sum < target) {
      left += 1;
    } else {
      return [nums[left], nums[right]];
    }
  }
  return [];
};
```
