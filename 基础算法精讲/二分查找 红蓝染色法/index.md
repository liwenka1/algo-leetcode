# 34. 在排序数组中查找元素的第一个和最后一个位置

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function (nums, target) {
  const n = nums.length;
  const lowerBound = (target) => {
    let left = 0;
    let right = n - 1;
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);
      if (nums[mid] < target) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
    return left;
  };
  const ansleft = lowerBound(target);
  const ansright = lowerBound(target + 1) - 1;
  return nums[ansleft] === target && nums[ansright] === target
    ? [ansleft, ansright]
    : [-1, -1];
};
```

# 2529. 正整数和负整数的最大计数

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maximumCount = function (nums) {
  const n = nums.length;
  const lowerBound = (target) => {
    let left = 0;
    let right = n - 1;
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);
      if (nums[mid] < target) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
    return left;
  };
  const start = lowerBound(0);
  const end = lowerBound(1);
  return Math.max(start, n - end);
};
```

# 2300. 咒语和药水的成功对数

```js
/**
 * @param {number[]} spells
 * @param {number[]} potions
 * @param {number} success
 * @return {number[]}
 */
var successfulPairs = function (spells, potions, success) {
  potions.sort((a, b) => a - b);
  const n = potions.length;
  const lowerBound = (spell) => {
    let left = 0;
    let right = n - 1;
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);
      if (potions[mid] * spell < success) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
    return left;
  };
  const ans = [];
  for (const spell of spells) {
    ans.push(n - lowerBound(spell));
  }
  return ans;
};
```

# 2563. 统计公平数对的数目

```js
/**
 * @param {number[]} nums
 * @param {number} lower
 * @param {number} upper
 * @return {number}
 */
var countFairPairs = function (nums, lower, upper) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const lowerBound = (right, target) => {
    let left = 0;
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);
      if (nums[mid] < target) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
    return left;
  };
  let ans = 0;
  for (let i = 0; i < n; i++) {
    const l = lowerBound(i - 1, lower - nums[i]);
    const r = lowerBound(i - 1, upper - nums[i] + 1);
    ans += r - l;
  }
  return ans;
};
```

# 275. H 指数 II

```js
/**
 * @param {number[]} citations
 * @return {number}
 */
var hIndex = function (citations) {
  const n = citations.length;
  let left = 0;
  let right = n - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (citations[mid] < n - mid) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return n - left;
};
```