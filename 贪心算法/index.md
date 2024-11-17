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

# 45. 跳跃游戏 II

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var jump = function (nums) {
  const n = nums.length;
  if (n === 1) {
    return 0;
  }
  let lastJumpEnd = 0;
  let cover = 0;
  let ans = 0;
  for (let i = 0; i < n; i++) {
    cover = Math.max(cover, i + nums[i]);
    if (i === lastJumpEnd) {
      ans++;
      lastJumpEnd = cover;
      if (lastJumpEnd >= n - 1) {
        return ans;
      }
    }
  }
};
```

# 1005. K 次取反后最大化的数组和

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var largestSumAfterKNegations = function (nums, k) {
  nums.sort((a, b) => Math.abs(b) - Math.abs(a));
  const n = nums.length;
  let sum = 0;
  for (let i = 0; i < n; i++) {
    if (nums[i] < 0 && k > 0) {
      nums[i] *= -1;
      k--;
    }
    sum += nums[i];
  }
  if (k % 2 === 1) {
    sum -= 2 * nums[n - 1];
  }
  return sum;
};
```

# 134. 加油站

```js
/**
 * @param {number[]} gas
 * @param {number[]} cost
 * @return {number}
 */
var canCompleteCircuit = function (gas, cost) {
  const n = gas.length;
  let cursum = 0;
  let totalsum = 0;
  let start = 0;
  for (let i = 0; i < n; i++) {
    totalsum += gas[i] - cost[i];
    cursum += gas[i] - cost[i];
    if (cursum < 0) {
      cursum = 0;
      start = i + 1;
    }
  }
  return totalsum >= 0 ? start : -1;
};
```

# 135. 分发糖果

```js
/**
 * @param {number[]} ratings
 * @return {number}
 */
var candy = function (ratings) {
  const n = ratings.length;
  const candy = new Array(n).fill(1);
  for (let i = 1; i < n; i++) {
    if (ratings[i] > ratings[i - 1]) {
      candy[i] = candy[i - 1] + 1;
    }
  }
  let ans = candy[n - 1];
  for (let i = n - 2; i >= 0; i--) {
    if (ratings[i] > ratings[i + 1]) {
      candy[i] = Math.max(candy[i], candy[i + 1] + 1);
    }
    ans += candy[i];
  }
  return ans;
};
```

# 860. 柠檬水找零

```js
/**
 * @param {number[]} bills
 * @return {boolean}
 */
var lemonadeChange = function (bills) {
  let fivecnt = 0;
  let tencnt = 0;
  for (const bill of bills) {
    if (bill === 5) {
      fivecnt++;
    } else if (bill === 10) {
      tencnt++;
      fivecnt--;
    } else if (bill === 20) {
      if (tencnt > 0) {
        tencnt--;
        fivecnt--;
      } else {
        fivecnt -= 3;
      }
    }
    if (fivecnt < 0) {
      return false;
    }
  }
  return true;
};
```

# 406. 根据身高重建队列

```js
/**
 * @param {number[][]} people
 * @return {number[][]}
 */
var reconstructQueue = function (people) {
  const queue = [];
  people.sort((a, b) => {
    if (a[0] === b[0]) {
      return a[1] - b[1];
    } else {
      return b[0] - a[0];
    }
  });
  const n = people.length;
  for (let i = 0; i < n; i++) {
    const [h, k] = people[i];
    queue.splice(k, 0, [h, k]);
  }
  return queue;
};
```

# 452. 用最少数量的箭引爆气球

```js
/**
 * @param {number[][]} points
 * @return {number}
 */
var findMinArrowShots = function (points) {
  points.sort((a, b) => a[0] - b[0]);
  const n = points.length;
  let ans = 1;
  for (let i = 1; i < n; i++) {
    if (points[i][0] > points[i - 1][1]) {
      ans++;
    } else {
      points[i][1] = Math.min(points[i][1], points[i - 1][1]);
    }
  }
  return ans;
};
```

# 435. 无重叠区间

```js
/**
 * @param {number[][]} intervals
 * @return {number}
 */
var eraseOverlapIntervals = function (intervals) {
  intervals.sort((a, b) => a[0] - b[0]);
  const n = intervals.length;
  let ans = 0;
  for (let i = 1; i < n; i++) {
    if (intervals[i][0] < intervals[i - 1][1]) {
      ans++;
      intervals[i][1] = Math.min(intervals[i - 1][1], intervals[i][1]);
    }
  }
  return ans;
};
```