### [剑指 Offer 57 - II. 和为 s 的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

**题目：** 输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

**示例 1：**

```
输入：target = 9
输出：[[2,3,4],[4,5]]
```

**示例 2：**

```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

**限制：** `1 <= target <= 10^5`

**题解一：暴力法（循环法）**

暴力循环法，分外内循环。

```js
var findContinuousSequence = function (target) {
  // 至少包含两个数，则 target 需大于 2
  if (target <= 2) {
    return [];
  }
  const limit = Math.ceil(target / 2);
  let sum = 0;
  const res = [];
  // 外循环
  for (let i = 1; i <= limit; i++) {
    sum += i;
    // 内循环
    for (let j = i + 1; j <= limit; j++) {
      sum += j;
      // 如果 sum 大于 target，清空 sum 进入下一个外循环
      if (sum > target) {
        sum = 0;
        break;
      } else if (sum === target) {
        let arr = [];
        for (let k = i; k <= j; k++) {
          arr.push(k);
        }
        res.push(arr);
        sum = 0;
        break;
      }
    }
  }
  return res;
};
```

复杂度分析：

- 时间复杂度：内外循环复杂度相乘，外循环复杂度为 target，内循环复杂度为根号 target
- 空间复杂度：O(1)

**题解二：滑动窗口**

- 当窗口的和小于 `target` 的时候，窗口的和需要增加，所以要扩大窗口，窗口的右边界向右移动。
- 当窗口的和大于 `target` 的时候，窗口的和需要减少，所以要缩小窗口，窗口的左边界向右移动。
- 当窗口的和恰好等于 `target` 的时候，我们需要记录此时的结果。设此时的窗口为 `[i, j]`，那么我们已经找到了一个 `i` 开头的序列，也是唯一一个 `i` 开头的序列，接下来需要找 `i+1` 开头的序列，所以窗口的左边界要向右移动。

```js
/**
 * @param {number} target
 * @return {number[][]}
 */
var findContinuousSequence = function (target) {
  // 至少包含两个数，则 target 需大于 2
  if (target <= 2) {
    return [];
  }
  // 滑动窗口左右指针
  let left = 1;
  let right = 2;
  // 右边界
  const limit = Math.ceil(target / 2);
  const res = [];
  // 记录当前窗口的和
  let sum = left + right;
  // 左指针 < 右指针，右指针 <= 右边界 （左指针 <= 右边界）
  while (left < right && right <= limit) {
    if (target > sum) {
      // 如果目标值（target） > 当前窗口的和（sum）
      // 右指针向右移动一个位置（right = right+1）
      right++;
      // 窗口的和加上当前右指针指向的值
      sum += right;
    } else if (target < sum) {
      // 如果目标值（target） < 当前窗口的和（sum）
      // 窗口的和减去当前左指针指向的值（left）
      sum -= left;
      // 左指针向右移动一个位置（left = left + 1）
      left++;
    } else {
      // 如果目标值（target） > 当前窗口的和（sum）
      let arr = [];
      for (let i = left; i <= right; i++) {
        arr.push(i);
      }
      // 把滑动窗口元素的数组 push 到结果中
      res.push(arr);
      // 窗口的和减去当前左指针指向的值（left）
      sum -= left;
      // 左指针向右移动一个位置（left = left + 1）
      left++;
    }
  }
  return res;
};
```

复杂度分析：

- 时间复杂度：O(n)
- 空间复杂度：O(1)
