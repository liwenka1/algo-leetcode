# 3111. 覆盖所有点的最少矩形数目

```js
/**
 * @param {number[][]} points
 * @param {number} w
 * @return {number}
 */
var minRectanglesToCoverPoints = function (points, w) {
  points.sort((a, b) => a[0] - b[0]);
  let ans = 0;
  let end = -1;
  for (const [x, _] of points) {
    if (x > end) {
      ans++;
      end = x + w;
    }
  }
  return ans;
};
```

# 1237. 找出给定方程的正整数解

```js
/**
 * // This is the CustomFunction's API interface.
 * // You should not implement it, or speculate about its implementation
 * function CustomFunction() {
 *     @param {integer, integer} x, y
 *     @return {integer}
 *     this.f = function(x, y) {
 *         ...
 *     };
 * };
 */

/**
 * @param {CustomFunction} customfunction
 * @param {integer} z
 * @return {integer[][]}
 */
var findSolution = function (customfunction, z) {
  let x = 1;
  let y = 1000;
  const ans = [];
  while (x <= 1000 && y >= 1) {
    const res = customfunction.f(x, y);
    if (res > z) {
      y--;
    } else if (res < z) {
      x++;
    } else {
      ans.push([x++, y--]);
    }
  }
  return ans;
};
```

# 3101. 交替子数组计数

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var countAlternatingSubarrays = function (nums) {
  let ans = 1;
  for (let start = 0, end = 1; end < nums.length; end++) {
    if (nums[end] === nums[end - 1]) {
      start = end;
    }
    ans += end - start + 1;
  }
  return ans;
};
```

# 2734. 执行子串操作后的字典序最小字符串

```js
/**
 * @param {string} s
 * @return {string}
 */
var smallestString = function (s) {
  const list = s.split("");
  const n = list.length;
  for (let i = 0; i < n; i++) {
    if (list[i] === "a") continue;
    for (let j = i; j < n && list[j] !== "a"; j++) {
      list[j] = String.fromCharCode(list[j].charCodeAt(0) - 1);
    }
    return list.join("");
  }
  list[n - 1] = "z";
  return list.join("");
};
```