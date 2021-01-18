### [142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

**题目：** 给定一个链表，返回链表开始入环的第一个节点。如果链表无环，则返回  `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 `0` 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。**注意：`pos` 仅仅是用于标识环的情况，并不会作为参数传递到函数中**。

说明：不允许修改给定的链表。

进阶：你是否可以使用 O(1) 空间解决此题？

示例 1：

![环形链表](../images/circularlinkedlist.png)

```
输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
```

示例  2：

![是否为环形链表](../images/circularlinkedlist-test2.png)

```
输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
```

示例 3：

![是否为环形链表](../images/circularlinkedlist-test3.png)

```
输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
```

提示：

- 链表中节点的数目范围在范围 `[0, 104]` 内
- `-105 <= Node.val <= 105`
- `pos` 的值为 `-1` 或者链表中的一个有效索引

**题解：快慢指针**

判断链表环路的问题，通用的解法为--**快慢指针(Floyd 判圈法)**。

给定两个指针 `slow` 和 `fast`，起始位置在链表的开头。每次 `fast` 前进两步，`slow` 前进一步。如果 `fast` 可以走到尽头，那么说明没有环路；如果 `fast` 可以无限走下去，说明一定有环路，且存在一个时刻 `slow` 和 `fast` 相遇。

当 `slow` 和 `fast` 第一次相遇时，将 `fast` 重新移动到链表开头，并让 `slow` 和 `fast` 每次都前进一步。当 `slow` 和 `fast` 第二次相遇时，相遇的节点即为环路的开始点。

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function (head) {
  if (head === null) {
    return null;
  }

  let fast = head;
  let slow = head;
  // 判断有环
  while (fast !== null && fast.next !== null) {
    fast = fast.next.next;
    slow = slow.next;
    // 第一次相遇时，将 `fast` 重新移动到链表开头，并让 `slow` 和 `fast` 每次都前进一步
    if (fast === slow) {
      fast = head;
      while (fast !== slow) {
        fast = fast.next;
        slow = slow.next;
      }
      // 二次相遇时，相遇的节点即为环路的开始点
      return fast;
    }
  }
  return null;
};
```

复杂度分析：

- 时间复杂度：O(n)，其中 n 为链表中节点的数目。在最初判断快慢指针是否相遇时，slow 指针走过的距离不会超过链表的总长度；随后寻找入环点时，走过的距离也不会超过链表的总长度。因此，总的执行时间为 O(n)+O(n)=O(n)。
- 空间复杂度：O(1)。我们只使用了 slow，fast 两个指针。

**题解二：哈希表（Set）**

遍历链表中的每个节点，并将它记录下来；一旦遇到了此前遍历过的节点，就可以判定链表中存在环。借助哈希表可以很方便地实现。

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */

/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var detectCycle = function (head) {
  const visited = new Set();
  while (head) {
    if (visited.has(head)) {
      return head;
    }
    visited.add(head);
    head = head.next;
  }
  return null;
};
```

复杂度分析：

- 时间复杂度：O(n)，其中 n 为链表中节点的数目。恰好需要访问链表中的每一个节点。
- 空间复杂度：O(n)，其中 n 为链表中节点的数目。需要将链表中的每个节点都保存在哈希表当中。
