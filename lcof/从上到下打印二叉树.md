### [面试题 32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

**题目：** 从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
[3],
[9,20],
[15,7]
]
```

提示：

1. `节点总数 <= 1000`

同：[二叉树的层次遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

**题解一：BFS**
```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */

var levelOrder = function(root) {
  let res = [], queue = [];
  if (root === null) return res;
  queue.push( root );
  while (queue.length > 0) {
    let size = queue.length, temp = [];
    while (size > 0) {
      let offer = queue.shift();
      if (offer === null) continue;
      temp.push( offer.val );
      if (offer.left) queue.push( offer.left );
      if (offer.right) queue.push( offer.right );
      size--;
    }
    res.push( [...temp] );
    temp = [];
  }
  
  return res;
};
```
时间复杂度是O(n)，空间复杂度是O(n)

**题解二：BFS+二维数组**

- 初始化 queue，用于存储当前层的节点
- 检查 queue 是否为空
    - 如果不为空：依次遍历当前 queue 内的所有节点，检查每个节点的左右子节点，将不为空的子节点放入 queue，继续循环
    - 如果为空：跳出循环

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function(root) {
  if (!root) return [];
  const queue = [root];
  // 存放遍历结果
  const res = [];
  // 代表当前层数
  let level = 0;
  while (queue.length) {
    // 第level层的遍历结果
    res[level] = [];
    // 第level层的节点数量
    let levelNum = queue.length;
    while (levelNum--) {
      const node = queue.shift();
      res[level].push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }

    level++;
  }
  return res;
};
```
时间复杂度是O(n)，空间复杂度是O(n)