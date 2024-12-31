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

# 875. 爱吃香蕉的珂珂

```js
/**
 * @param {number[]} piles
 * @param {number} h
 * @return {number}
 */
var minEatingSpeed = function (piles, h) {
  let left = 0;
  let right = Math.max(...piles);
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    let sum = 0;
    for (const p of piles) {
      sum += Math.ceil(p / mid);
    }
    if (sum > h) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return left;
};
```

# 2187. 完成旅途的最少时间

```js
/**
 * @param {number[]} time
 * @param {number} totalTrips
 * @return {number}
 */
var minimumTime = function (time, totalTrips) {
  const min = Math.min(...time);
  let left = 0;
  let right = min * totalTrips;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    let sum = 0;
    for (const t of time) {
      sum += Math.floor(mid / t);
    }
    if (sum < totalTrips) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return left;
};
```

# 2861. 最大合金数

```js
/**
 * @param {number} n
 * @param {number} k
 * @param {number} budget
 * @param {number[][]} composition
 * @param {number[]} stock
 * @param {number[]} cost
 * @return {number}
 */
var maxNumberOfAlloys = function (n, k, budget, composition, stock, cost) {
  const check = (num, comp) => {
    let money = 0;
    for (let i = 0; i < n; i++) {
      if (stock[i] < comp[i] * num) {
        money += (comp[i] * num - stock[i]) * cost[i];
        if (money > budget) {
          return false;
        }
      }
    }
    return true;
  };
  const max = Math.min(...stock) + budget;
  let ans = 0;
  for (const comp of composition) {
    let left = ans;
    let right = max + 1;
    while (left + 1 < right) {
      const mid = Math.floor((left + right) / 2);
      if (check(mid, comp)) {
        left = mid;
      } else {
        right = mid;
      }
    }
    ans = left;
  }
  return ans;
};
```

# 2439. 最小化数组中的最大值

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var minimizeArrayValue = function (nums) {
  const n = nums.length;
  const check = (limit) => {
    let extra = 0;
    for (let i = n - 1; i > 0; i--) {
      extra = Math.max(nums[i] + extra - limit, 0);
    }
    return nums[0] + extra <= limit;
  };
  let left = 0;
  let right = Math.max(...nums);
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (check(mid)) {
      right = mid - 1;
    } else {
      left = mid + 1;
    }
  }
  return left;
};
```

# 2517. 礼盒的最大甜蜜度

```js
/**
 * @param {number[]} price
 * @param {number} k
 * @return {number}
 */
var maximumTastiness = function (price, k) {
  price.sort((a, b) => a - b);
  const check = (mid) => {
    let cnt = 1;
    let pre = price[0];
    for (const p of price) {
      if (p >= pre + mid) {
        cnt++;
        pre = p;
      }
    }
    return cnt;
  };
  const n = price.length;
  let left = 0;
  let right = Math.max(...price) - Math.min(...price);
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);
    if (check(mid) >= k) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return right;
};
```