### [面试题 54. 二叉搜索树的第 k 大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

**题目：** 给定一棵二叉搜索树，请找出其中第 k 大的节点。

示例 1:

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```

示例 2:

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

限制：

```
1 ≤ k ≤ 二叉搜索树元素个数
```

**题解一：中序遍历**

分析题目知道我们要把树节点从大到小排列，然后取出第 k 个节点的值，就可以了。那怎么让树节点。

下面有两个要点：

- 我们知道二叉树的特点是节点值大小顺序是 左 < 中 < 右。
- 中序遍历(In-Order Traversal)，指先访问左（右）子树，然后访问根，最后访问右（左）子树的遍历方式。

所以我们采用中序遍历且先访问大的节点即右节点。

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
 * @param {number} k
 * @return {number}
 */
var kthLargest = function(root, k) {
  let res = [];
  const inOrderTraversal = node => {
    if (node === null) {
      return null;
    }
    // 右
    inOrderTraversal(node.right);
    // 中
    res.push(node);
    // 左
    inOrderTraversal(node.left);
  };
  inOrderTraversal(root);
  return res[k - 1].val;
};
```

**题解二：栈**

```js
var kthLargest = function(root, k) {
  const res = [],
    stack = [];
  let node = root;
  while (stack.length > 0 || node !== null) {
    if (node) {
      stack.push(node);
      // 先右
      node = node.right;
    } else {
      node = stack.pop();
      // 存储
      res.push(node.val);
      // 后左
      node = node.left;
    }
  }
  return res[k - 1];
};
```

**题解三：优化栈**

当个数正好等于 k 的时候返回值。

```js
var kthLargest = function(root, k) {
  const stack = [];
  let node = root;
  let count = 0;
  while (stack.length > 0 || node !== null) {
    if (node) {
      stack.push(node);
      node = node.right;
    } else {
      node = stack.pop();
      count++;
      if (count >= k) {
        return node.val;
      }
      node = node.left;
    }
  }
  return 0;
};
```
