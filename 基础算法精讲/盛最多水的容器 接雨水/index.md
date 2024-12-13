# 11. 盛最多水的容器

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function (height) {
  const n = height.length;
  let left = 0;
  let right = n - 1;
  let ans = 0;
  while (left < right) {
    if (height[left] > height[right]) {
      ans = Math.max(ans, (right - left) * height[right]);
      right--;
    } else {
      ans = Math.max(ans, (right - left) * height[left]);
      left++;
    }
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
  const pre = new Array(n).fill(0);
  pre[0] = height[0];
  for (let i = 1; i < n; i++) {
    pre[i] = Math.max(pre[i - 1], height[i]);
  }
  const suf = new Array(n).fill(0);
  suf[n - 1] = height[n - 1];
  for (let i = n - 2; i >= 0; i--) {
    suf[i] = Math.max(suf[i + 1], height[i]);
  }
  let ans = 0;
  for (let i = 0; i < n; i++) {
    ans += Math.min(pre[i], suf[i]) - height[i];
  }
  return ans;
};
```

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function (height) {
  const n = height.length;
  let left = 0;
  let right = n - 1;
  let premax = height[0];
  let sufmax = height[n - 1];
  let ans = 0;
  while (left < right) {
    premax = Math.max(premax, height[left]);
    sufmax = Math.max(sufmax, height[right]);
    if (premax < sufmax) {
      ans += premax - height[left];
      left++;
    } else {
      ans += sufmax - height[right];
      right--;
    }
  }
  return ans;
};
```