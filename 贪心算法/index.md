# 455. 分发饼干

```js
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function (g, s) {
  g.sort((a, b) => a - b);
  s.sort((a, b) => a - b);
  const n = g.length;
  const m = s.length;
  let i = n - 1;
  let j = m - 1;
  let ans = 0;
  while (i >= 0 && j >= 0) {
    if (s[j] < g[i]) {
      i--;
    } else {
      ans++;
      i--;
      j--;
    }
  }
  return ans;
};
```

```js
/**
 * @param {number[]} g
 * @param {number[]} s
 * @return {number}
 */
var findContentChildren = function (g, s) {
  g.sort((a, b) => a - b);
  s.sort((a, b) => a - b);
  const n = g.length;
  const m = s.length;
  let i = 0;
  let j = 0;
  let ans = 0;
  while (i < n && j < m) {
    if (s[j] < g[i]) {
      j++;
    } else {
      ans++;
      i++;
      j++;
    }
  }
  return ans;
};
```

# 376. 摆动序列

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var wiggleMaxLength = function (nums) {
  const n = nums.length;
  if (n === 1) {
    return 1;
  }
  if (n === 2 && nums[0] !== nums[1]) {
    return 2;
  }
  let prediff = 0;
  let ans = 1;
  for (let i = 0; i < n - 1; i++) {
    const curdiff = nums[i + 1] - nums[i];
    if ((prediff <= 0 && curdiff > 0) || (prediff >= 0 && curdiff < 0)) {
      ans++;
      prediff = curdiff;
    }
  }
  return ans;
};
```

# 53. 最大子数组和

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
  const n = nums.length;
  let sum = 0;
  let ans = -Infinity;
  for (let i = 0; i < n; i++) {
    sum += nums[i];
    if (sum > ans) {
      ans = sum;
    }
    if (sum < 0) {
      sum = 0;
    }
  }
  return ans;
};
```

# 122. 买卖股票的最佳时机 II

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  const n = prices.length;
  let ans = 0;
  for (let i = 1; i < n; i++) {
    if (prices[i] - prices[i - 1] > 0) {
      ans += prices[i] - prices[i - 1];
    }
  }
  return ans;
};
```

# 55. 跳跃游戏

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canJump = function (nums) {
  const n = nums.length;
  if (n === 1) {
    return true;
  }
  let cover = 0;
  for (let i = 0; i < n; i++) {
    if (cover >= i) {
      cover = Math.max(i + nums[i], cover);
    }
    if (cover >= n - 1) {
      return true;
    }
  }
  return false;
};
```