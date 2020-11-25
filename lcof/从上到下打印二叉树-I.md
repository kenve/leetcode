### [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

**题目：** 从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回：

```
[3,9,20,15,7]
```

提示：

1. `节点总数 <= 1000`

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
 * @return {number[]}
 */
var levelOrder = function (root) {
  if (root == null) {
    return [];
  }
  let queue = [root];
  const res = [];
  while (queue.length) {
    const node = queue.shift();
    res.push(node.val);
    // console.log(node.val);
    if (node.left) {
      queue.push(node.left);
    }
    if (node.right) {
      queue.push(node.right);
    }
  }
  return res;
};
```

复杂度分析：

- 时间复杂度：O(n)，n 为二叉树的节点数量，即 BFS 需循环 n 次。
- 空间复杂度：O(n)，最差情况下，即当树为平衡二叉树时，最多有 n/2 个树节点同时在 queue 中，使用 O(n) 大小的额外空间。
