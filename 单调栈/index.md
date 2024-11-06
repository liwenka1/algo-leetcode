# 739. 每日温度

```js
/**
 * @param {number[]} temperatures
 * @return {number[]}
 */
var dailyTemperatures = function (temperatures) {
  const n = temperatures.length;
  const stack = [0];
  const ans = new Array(n).fill(0);
  for (let i = 1; i < n; i++) {
    while (
      stack.length &&
      temperatures[i] > temperatures[stack[stack.length - 1]]
    ) {
      const j = stack.pop();
      ans[j] = i - j;
    }
    stack.push(i);
  }
  return ans;
};
```

# 496. 下一个更大元素 I

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var nextGreaterElement = function (nums1, nums2) {
  const map = new Map();
  for (const i in nums1) {
    map.set(nums1[i], i);
  }
  const m = nums1.length;
  const n = nums2.length;
  const stack = [0];
  const ans = new Array(m).fill(-1);
  for (let i = 1; i < n; i++) {
    while (stack.length && nums2[i] > nums2[stack[stack.length - 1]]) {
      const j = stack.pop();
      if (map.has(nums2[j])) {
        ans[map.get(nums2[j])] = nums2[i];
      }
    }
    stack.push(i);
  }
  return ans;
};
```

# 503. 下一个更大元素 II

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var nextGreaterElements = function (nums) {
  const n = nums.length;
  const stack = [0];
  const ans = new Array(n).fill(-1);
  for (let i = 1; i < 2 * n; i++) {
    while (stack.length && nums[i % n] > nums[stack[stack.length - 1]]) {
      const j = stack.pop();
      ans[j % n] = nums[i % n];
    }
    stack.push(i % n);
  }
  return ans;
};
```

# 42. 接雨水

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function (height) {
  const n = height.length;
  const stack = [0];
  let ans = 0;
  for (let i = 1; i < n; i++) {
    while (stack.length && height[i] > height[stack[stack.length - 1]]) {
      const mid = stack.pop();
      if (stack.length) {
        const left = stack[stack.length - 1];
        const h = Math.min(height[left], height[i]) - height[mid];
        const w = i - left - 1;
        ans += h * w;
      }
    }
    stack.push(i);
  }
  return ans;
};
```

# 84. 柱状图中最大的矩形

```js
/**
 * @param {number[]} heights
 * @return {number}
 */
var largestRectangleArea = function (heights) {
  heights = [0, ...heights, 0];
  const n = heights.length;
  const stack = [0];
  let ans = 0;
  for (let i = 1; i < n; i++) {
    while (stack.length && heights[i] < heights[stack[stack.length - 1]]) {
      const mid = stack.pop();
      if (stack.length) {
        const left = stack[stack.length - 1];
        const h = heights[mid];
        const w = i - left - 1;
        ans = Math.max(ans, h * w);
      }
    }
    stack.push(i);
  }
  return ans;
};
```
