# 209. 长度最小的子数组

```js
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function (target, nums) {
  const n = nums.length;
  let sum = 0;
  let ans = Infinity;
  for (let left = 0, right = 0; right < n; right++) {
    sum += nums[right];
    while (sum >= target) {
      ans = Math.min(ans, right - left + 1);
      sum -= nums[left];
      left++;
    }
  }
  return ans === Infinity ? 0 : ans;
};
```

# 3. 无重复字符的最长子串

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  const n = s.length;
  const map = new Map();
  let ans = 0;
  for (let left = 0, right = 0; right < n; right++) {
    map.set(s[right], (map.get(s[right]) || 0) + 1);
    while (map.get(s[right]) > 1) {
      map.set(s[left], map.get(s[left]) - 1);
      left++;
    }
    ans = Math.max(ans, right - left + 1);
  }
  return ans;
};
```

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  const n = s.length;
  const set = new Set();
  let ans = 0;
  for (let left = 0, right = 0; right < n; right++) {
    while (set.has(s[right])) {
      set.delete(s[left]);
      left++;
    }
    set.add(s[right]);
    ans = Math.max(ans, right - left + 1);
  }
  return ans;
};
```

# 713. 乘积小于 K 的子数组

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var numSubarrayProductLessThanK = function (nums, k) {
  if (k <= 1) {
    return 0;
  }
  const n = nums.length;
  let prod = 1;
  let ans = 0;
  for (let left = 0, right = 0; right < n; right++) {
    prod *= nums[right];
    while (prod >= k) {
      prod /= nums[left];
      left++;
    }
    ans += right - left + 1;
  }
  return ans;
};
```

# 2958. 最多 K 个重复元素的最长子数组

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maxSubarrayLength = function (nums, k) {
  const n = nums.length;
  const map = new Map();
  let ans = 0;
  for (let left = 0, right = 0; right < n; right++) {
    map.set(nums[right], (map.get(nums[right]) || 0) + 1);
    while (map.get(nums[right]) > k) {
      map.set(nums[left], map.get(nums[left]) - 1);
      left++;
    }
    ans = Math.max(ans, right - left + 1);
  }
  return ans;
};
```

# 2730. 找到最长的半重复子字符串

```js
/**
 * @param {string} s
 * @return {number}
 */
var longestSemiRepetitiveSubstring = function (s) {
  const n = s.length;
  const path = [];
  let k = 0;
  let ans = 0;
  for (let left = 0, right = 0; right < n; right++) {
    path.push(s[right]);
    if (right > 0 && s[right] === s[right - 1]) {
      k++;
    }
    while (k > 1) {
      path.shift();
      if (s[left] === s[left + 1]) {
        k--;
      }
      left++;
    }
    ans = Math.max(ans, right - left + 1);
  }
  return ans;
};
```

# 2779. 数组的最大美丽值

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var maximumBeauty = function (nums, k) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  let ans = 0;
  for (let left = 0, right = 0; right < n; right++) {
    while (right > 0 && Math.abs(nums[right] - nums[left]) > 2 * k) {
      left++;
    }
    ans = Math.max(ans, right - left + 1);
  }
  return ans;
};
```