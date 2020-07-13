### [350. 两个数组的交集 II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

**题目：** 给定两个数组，编写一个函数来计算它们的交集。
给定两个数组，编写一个函数来计算它们的交集。

**示例 1：**

```
输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2,2]
```

**示例 2:**

```
输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[4,9]
```

**说明：**

- 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。
- 我们可以不考虑输出结果的顺序。

**进阶：**

- 如果给定的数组已经排好序呢？你将如何优化你的算法？
- 如果 `nums1` 的大小比 `nums2` 小很多，哪种方法更优？
- 如果 `nums2` 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？

**题解一：Map**

- 实例化一个 Map 对象，用于存储其中一个数组的元素的个数，键（key）为元素值，值（value）为该元素的个数。
- 遍历第一个数组，判断如果元素值存在于 Map 对象中且个数大于等于 `1`，将该元素保存起来，并且 Map 中的个数减 `1`。
- 遍历完成，返回保存交集元素的数组。

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersect = function (nums1, nums2) {
  const len1 = nums1.length;
  const len2 = nums2.length;
  // 其中一个为空，直接返回空数组
  if (!len1 || !len2) {
    return [];
  }
  // 实例化 map 对象
  const map = new Map();
  // 遍历存储 nums1 的元素和个数
  for (let i = 0; i < len1; i++) {
    map.get(nums1[i]) ? map.set(nums1[i], map.get(nums1[i]) + 1) : map.set(nums1[i], 1);
  }
  const arr = [];
  // 遍历判断元素是否存在 map 对像中且个数大于 0
  for (let j = 0; j < len2; j++) {
    if (map.get(nums2[j]) >= 1) {
      mergeNums.push(nums2[j]);
      map.set(nums2[j], map.get(nums2[j]) - 1);
    }
  }
  return arr;
};
```

**复杂度分析：**

- 时间复杂度：O(m+n)，其中 m 和 n 分别是两个数组的长度。需要遍历两个数组并对哈希表进行操作，哈希表操作的时间复杂度是 O(1)，因此总时间复杂度与两个数组的长度和呈线性关系。

- 空间复杂度：O(min(m,n))，其中 m 和 n 分别是两个数组的长度。对较短的数组进行哈希表的操作，哈希表的大小不会超过较短的数组的长度。为返回值创建一个数组 `arr`，其长度为较短的数组的长度。

**题解二：排序**

- 排序两个数组，两个数组分别定义两个下标作为数组指针。
- 遍历数组
  - 如果 `nums1` 数组中的元素大于 `nums2` 的元素，则 `nums2` 的下标加 `1`
  - 如果 `nums1` 数组中的元素小于 `nums2` 的元素，则 `nums1` 的下标加 `1`
  - 如果 `nums1` 数组中的元素等于 `nums2` 的元素，则 `nums1` 和 `nums2` 的下标都加 `1`，并把相等的元素值，保存到交集数组中。
- 当其中一个数组遍历完成（指针指向最后），退出。

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersect = function (nums1, nums2) {
  const len1 = nums1.length;
  const len2 = nums2.length;
  if (!len1 || !len2) {
    return [];
  }
  // 排序数组
  nums1.sort((a, b) => a - b);
  nums2.sort((a, b) => a - b);
  // 数组 nums1 的下标
  let i1 = 0;
  // 数组 nums2 的下标
  let i2 = 0;
  let arr = [];
  // 遍历知道其中一个数组所有元素遍历完
  while (i1 < len1 && i2 < len2) {
    // 如果 nums1 数组中的元素大于 nums2 的元素，则 nums2 的下标加 1
    if (nums1[i1] > nums2[i2]) {
      i2++;
    } else if (nums1[i1] < nums2[i2]) {
      // 如果 nums1 数组中的元素小于 nums2 的元素，则 nums1 的下标加 1
      i1++;
    } else {
      // 如果 nums1 数组中的元素等于 nums2 的元素，则 nums1 和 nums2 的下标都加 1
      // 并把相等的元素值，保存到交集数组中
      arr.push(nums1[i1]);
      i1++;
      i2++;
    }
  }
  return arr;
};
```

复杂度分析

时间复杂度：O(mlogm + nlogn)，其中 m 和 n 分别是两个数组的长度。对两个数组进行排序的时间复杂度是 O(mlogm + nlogn)，遍历两个数组的时间复杂度是 O(m+n)，因此总时间复杂度是 O(mlogm + nlogn)。

空间复杂度：O(min(m,n))，其中 m 和 n 分别是两个数组的长度。为返回值创建一个数组 `intersection`，其长度为较短的数组的长度。
