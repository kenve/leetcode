### [剑指 Offer 30. 包含 min 函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

同 [155. 最小栈](https://leetcode-cn.com/problems/min-stack/)

**题目：** 定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

示例:

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.
```

提示：各函数的调用总次数不超过 20000 次

**题解：辅助栈**

总体思路都是在入栈的同时设法保存当前栈中的最小值，可以用额外的辅助栈实现，也可以使用链表实现栈并且在链表节点中存储当前栈的最小值，再或者栈中元素是一个对象 `{x: min(x, 当前栈内最小值)}`。

![剑指 Offer 30. 包含 min 函数的栈](../images/min-stack.gif)

```ts
class MinStack {
  constructor() {}

  // 元素值
  xstack: number[] = [];
  // 最小值栈，默认最小值为无限大
  mstack: number[] = [Infinity];

  push(x: number): void {
    // 入栈
    this.xstack.push(x);
    // 当前最小值，压入最小值栈
    this.mstack.push(Math.min(this.mstack[this.mstack.length - 1], x));
  }

  pop(): void {
    this.mstack.pop();
    this.xstack.pop();
  }

  top(): number {
    return this.xstack[this.xstack.length - 1];
  }

  min(): number {
    return this.mstack[this.mstack.length - 1];
  }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(x)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.min()
 */
```

复杂度分析：

- 时间复杂度：对于题目中的所有操作，时间复杂度均为 O(1)。因为栈的插入、删除与读取操作都是 O(1)，我们定义的每个操作最多调用栈操作两次。
- 空间复杂度：O(n)，其中 n 为总操作数。最坏情况下，我们会连续插入 n 个元素，此时两个栈占用的空间为 O(n)。
