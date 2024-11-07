# 232. 用栈实现队列

```js
var MyQueue = function () {
  this.stackin = [];
  this.stackout = [];
};

/**
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function (x) {
  this.stackin.push(x);
};

/**
 * @return {number}
 */
MyQueue.prototype.pop = function () {
  if (!this.stackout.length) {
    while (this.stackin.length) {
      this.stackout.push(this.stackin.pop());
    }
  }
  return this.stackout.pop();
};

/**
 * @return {number}
 */
MyQueue.prototype.peek = function () {
  const x = this.pop();
  this.stackout.push(x);
  return x;
};

/**
 * @return {boolean}
 */
MyQueue.prototype.empty = function () {
  return !this.stackin.length && !this.stackout.length;
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```

# 225. 用队列实现栈

```js
var MyStack = function () {
  this.queue = [];
};

/**
 * @param {number} x
 * @return {void}
 */
MyStack.prototype.push = function (x) {
  this.queue.push(x);
};

/**
 * @return {number}
 */
MyStack.prototype.pop = function () {
  for (let i = 0; i < this.queue.length - 1; i++) {
    this.queue.push(this.queue.shift());
  }
  return this.queue.shift();
};

/**
 * @return {number}
 */
MyStack.prototype.top = function () {
  const x = this.pop();
  this.queue.push(x);
  return x;
};

/**
 * @return {boolean}
 */
MyStack.prototype.empty = function () {
  return !this.queue.length;
};

/**
 * Your MyStack object will be instantiated and called as such:
 * var obj = new MyStack()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.empty()
 */
```

# 20. 有效的括号

```js
/**
 * @param {charing} s
 * @return {boolean}
 */
var isValid = function (s) {
  const n = s.length;
  if (n % 2 !== 0) {
    return false;
  }
  const stack = [];
  const left = ["(", "{", "["];
  const map = {
    "(": ")",
    "{": "}",
    "[": "]",
  };
  for (const char of s) {
    if (left.includes(char)) {
      stack.push(char);
    } else {
      // 如果栈为空或匹配失败，则返回 false
      // 如果栈为空，stack.pop() 将返回 undefined
      if (map[stack.pop()] !== char) {
        return false;
      }
    }
  }
  return !stack.length;
};
```

# 1047. 删除字符串中的所有相邻重复项

```js
/**
 * @param {string} s
 * @return {string}
 */
var removeDuplicates = function (s) {
  const stack = [];
  for (const char of s) {
    if (stack.length && stack[stack.length - 1] === char) {
      stack.pop();
    } else {
      stack.push(char);
    }
  }
  return stack.join("");
};
```

# 150. 逆波兰表达式求值

```js
/**
 * @param {string[]} tokens
 * @return {number}
 */
var evalRPN = function (tokens) {
  const stack = [];
  for (const token of tokens) {
    if (token === "+" || token === "-" || token === "*" || token === "/") {
      const y = stack.pop();
      const x = stack.pop();
      if (token === "+") {
        stack.push(x + y);
      } else if (token === "-") {
        stack.push(x - y);
      } else if (token === "*") {
        stack.push(x * y);
      } else if (token === "/") {
        stack.push(Math.trunc(x / y));
      }
    } else {
      stack.push(Number(token));
    }
  }
  return stack.pop();
};
```

# 239. 滑动窗口最大值

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var maxSlidingWindow = function (nums, k) {
  const n = nums.length;
  const deque = [];
  const ans = [];
  for (let i = 0; i < n; i++) {
    if (deque.length && deque[0] < i - k + 1) {
      deque.shift();
    }
    while (deque.length && nums[i] > nums[deque[deque.length - 1]]) {
      deque.pop();
    }
    deque.push(i);
    if (i >= k - 1) {
      ans.push(nums[deque[0]]);
    }
  }
  return ans;
};
```

# 347. 前 K 个高频元素

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function (nums, k) {
  const map = new Map();
  for (let num of nums) {
    map.set(num, (map.get(num) || 0) + 1);
  }
  return [...map.entries()]
    .sort((a, b) => b[1] - a[1])
    .slice(0, k)
    .map((i) => i[0]);
};
```