# 704. 二分查找

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  const n = nums.length;
  let left = 0;
  let right = n - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (target < nums[mid]) {
      right = mid - 1;
    } else if (target > nums[mid]) {
      left = mid + 1;
    } else {
      return mid;
    }
  }
  return -1;
};
```

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  const n = nums.length;
  let left = 0;
  let right = n;
  while (left < right) {
    const mid = Math.floor((left + right) / 2);
    if (target < nums[mid]) {
      right = mid;
    } else if (target > nums[mid]) {
      left = mid + 1;
    } else {
      return mid;
    }
  }
  return -1;
};
```

# 27. 移除元素

```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function (nums, val) {
  const n = nums.length;
  let slow = 0;
  for (let fast = 0; fast < n; fast++) {
    if (nums[fast] !== val) {
      nums[slow++] = nums[fast];
    }
  }
  return slow;
};
```

# 977. 有序数组的平方

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var sortedSquares = function (nums) {
  const n = nums.length;
  let left = 0;
  let right = n - 1;
  let k = n - 1;
  const ans = new Array(n).fill(0);
  while (left <= right) {
    const num_left = nums[left] * nums[left];
    const num_right = nums[right] * nums[right];
    if (num_left >= num_right) {
      ans[k--] = num_left;
      left++;
    } else {
      ans[k--] = num_right;
      right--;
    }
  }
  return ans;
};
```

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
      sum -= nums[left++];
    }
  }
  return ans === Infinity ? 0 : ans;
};
```

# 59. 螺旋矩阵 II

```js
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function (n) {
  const mid = Math.floor(n / 2);
  let loop = mid;
  let startx = 0;
  let starty = 0;
  let offset = 1;
  let cnt = 1;
  const ans = Array.from({ length: n }, () => new Array(n).fill(0));
  while (loop--) {
    let i = startx;
    let j = starty;
    while (j < n - offset) {
      ans[i][j++] = cnt++;
    }
    while (i < n - offset) {
      ans[i++][j] = cnt++;
    }
    while (j >= offset) {
      ans[i][j--] = cnt++;
    }
    while (i >= offset) {
      ans[i--][j] = cnt++;
    }
    startx++;
    starty++;
    offset++;
  }
  if (n % 2 === 1) {
    ans[mid][mid] = n * n;
  }
  return ans;
};
```