# 203. 移除链表元素

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function (head, val) {
  while (head !== null && head.val === val) {
    head = head.next;
  }
  let cur = head;
  while (cur !== null && cur.next !== null) {
    if (cur.next.val === val) {
      cur.next = cur.next.next;
    } else {
      cur = cur.next;
    }
  }
  return head;
};
```

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} val
 * @return {ListNode}
 */
var removeElements = function (head, val) {
  let dummyhead = new ListNode();
  dummyhead.next = head;
  let cur = dummyhead;
  while (cur.next !== null) {
    if (cur.next.val === val) {
      cur.next = cur.next.next;
    } else {
      cur = cur.next;
    }
  }
  return dummyhead.next;
};
```

# 707. 设计链表

```js
var MyLinkedList = function () {
  this.size = 0;
  this.head = new ListNode(0);
};

/**
 * @param {number} index
 * @return {number}
 */
MyLinkedList.prototype.get = function (index) {
  if (index < 0 || index >= this.size) {
    return -1;
  }
  let cur = this.head;
  while (index--) {
    cur = cur.next;
  }
  return cur.next.val;
};

/**
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtHead = function (val) {
  this.addAtIndex(0, val);
};

/**
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtTail = function (val) {
  this.addAtIndex(this.size, val);
};

/**
 * @param {number} index
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtIndex = function (index, val) {
  if (index > this.size) {
    return;
  }
  this.size++;
  let cur = this.head;
  while (index--) {
    cur = cur.next;
  }
  let newnode = new ListNode(val);
  newnode.next = cur.next;
  cur.next = newnode;
};

/**
 * @param {number} index
 * @return {void}
 */
MyLinkedList.prototype.deleteAtIndex = function (index) {
  if (index < 0 || index >= this.size) {
    return;
  }
  this.size--;
  let cur = this.head;
  while (index--) {
    cur = cur.next;
  }
  cur.next = cur.next.next;
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * var obj = new MyLinkedList()
 * var param_1 = obj.get(index)
 * obj.addAtHead(val)
 * obj.addAtTail(val)
 * obj.addAtIndex(index,val)
 * obj.deleteAtIndex(index)
 */
```

# 206. 反转链表

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function (head) {
  let cur = head;
  let pre = null;
  while (cur !== null) {
    const temp = cur.next;
    cur.next = pre;
    pre = cur;
    cur = temp;
  }
  return pre;
};
```

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function (head) {
  const reverse = (cur, pre) => {
    if (cur === null) {
      return pre;
    }
    const temp = cur.next;
    cur.next = pre;
    return reverse(temp, cur);
  };
  return reverse(head, null);
};
```

# 24. 两两交换链表中的节点

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var swapPairs = function (head) {
  let dummyhead = new ListNode();
  dummyhead.next = head;
  let cur = dummyhead;
  while (cur.next && cur.next.next) {
    const firstNode = cur.next;
    const secondNode = cur.next.next;

    firstNode.next = secondNode.next;
    secondNode.next = firstNode;
    cur.next = secondNode;

    cur = firstNode;
  }
  return dummyhead.next;
};
```

# 19. 删除链表的倒数第 N 个结点

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
  let dummyhead = new ListNode();
  dummyhead.next = head;
  let slow = dummyhead;
  let fast = dummyhead;
  while (fast && n >= 0) {
    fast = fast.next;
    n--;
  }
  while (fast) {
    slow = slow.next;
    fast = fast.next;
  }
  slow.next = slow.next.next;
  return dummyhead.next;
};
```