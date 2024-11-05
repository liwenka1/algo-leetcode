# 509. 斐波那契数

```js
/**
 * @param {number} n
 * @return {number}
 */
var fib = function (n) {
  if (n === 0) {
    return 0;
  }
  const dp = new Array(n).fill(0);
  dp[0] = 1;
  dp[1] = 1;
  for (let i = 2; i < n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n - 1];
};
```

# 70. 爬楼梯

```js
/**
 * @param {number} n
 * @return {number}
 */
var climbStairs = function (n) {
  const dp = new Array(n).fill(0);
  dp[0] = 1;
  dp[1] = 2;
  for (let i = 2; i < n; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }
  return dp[n - 1];
};
```

# 746. 使用最小花费爬楼梯

```js
/**
 * @param {number[]} cost
 * @return {number}
 */
var minCostClimbingStairs = function (cost) {
  const n = cost.length;
  const dp = new Array(n + 1).fill(0);
  for (let i = 2; i <= n; i++) {
    dp[i] = Math.min(dp[i - 1] + cost[i - 1], dp[i - 2] + cost[i - 2]);
  }
  return dp[n];
};
```

# 62. 不同路径

```js
/**
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var uniquePaths = function (m, n) {
  const dp = Array.from({ length: n }, () => new Array(m).fill(0));
  for (let i = 0; i < n; i++) {
    dp[i][0] = 1;
  }
  for (let j = 0; j < m; j++) {
    dp[0][j] = 1;
  }
  for (let i = 1; i < n; i++) {
    for (let j = 1; j < m; j++) {
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    }
  }
  return dp[n - 1][m - 1];
};
```

# 63. 不同路径 II

```js
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function (obstacleGrid) {
  const n = obstacleGrid.length;
  const m = obstacleGrid[0].length;
  const dp = Array.from({ length: n }, () => new Array(m).fill(0));
  for (let i = 0; i < n && obstacleGrid[i][0] === 0; i++) {
    dp[i][0] = 1;
  }
  for (let j = 0; j < m && obstacleGrid[0][j] === 0; j++) {
    dp[0][j] = 1;
  }
  for (let i = 1; i < n; i++) {
    for (let j = 1; j < m; j++) {
      if (obstacleGrid[i][j] === 0) {
        dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
      }
    }
  }
  return dp[n - 1][m - 1];
};
```

# 343. 整数拆分

```js
/**
 * @param {number} n
 * @return {number}
 */
var integerBreak = function (n) {
  const dp = new Array(n + 1).fill(0);
  dp[2] = 1;
  for (let i = 3; i <= n; i++) {
    for (let j = 1; j <= i / 2; j++) {
      dp[i] = Math.max(dp[i], j * dp[i - j], j * (i - j));
    }
  }
  return dp[n];
};
```

# 96. 不同的二叉搜索树

```js
/**
 * @param {number} n
 * @return {number}
 */
var numTrees = function (n) {
  const dp = new Array(n + 1).fill(0);
  dp[0] = 1;
  dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    for (let j = 0; j < i; j++) {
      dp[i] += dp[j] * dp[i - j - 1];
    }
  }
  return dp[n];
};
```

```js
/**
 * @param {number} n
 * @return {number}
 */
var numTrees = function (n) {
  const dp = new Array(n + 1).fill(0);
  dp[0] = 1;
  dp[1] = 1;
  for (let i = 2; i <= n; i++) {
    for (let j = 1; j <= i; j++) {
      dp[i] += dp[j - 1] * dp[i - j];
    }
  }
  return dp[n];
};
```

# 416. 分割等和子集

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var canPartition = function (nums) {
  const sum = nums.reduce((a, b) => a + b);
  if (sum % 2 !== 0) {
    return false;
  }
  const target = sum / 2;
  const n = nums.length;
  const dp = new Array(target + 1).fill(0);
  for (let i = 0; i < n; i++) {
    for (let j = target; j >= nums[i]; j--) {
      dp[j] = Math.max(dp[j], dp[j - nums[i]] + nums[i]);
    }
  }
  return dp[target] === target;
};
```

# 1049. 最后一块石头的重量 II

```js
/**
 * @param {number[]} stones
 * @return {number}
 */
var lastStoneWeightII = function (stones) {
  const sum = stones.reduce((a, b) => a + b);
  const target = Math.floor(sum / 2);
  const n = stones.length;
  const dp = new Array(target + 1).fill(0);
  for (let i = 0; i < n; i++) {
    for (let j = target; j >= stones[i]; j--) {
      dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
    }
  }
  return sum - 2 * dp[target];
};
```

# 494. 目标和

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var findTargetSumWays = function (nums, target) {
  const sum = nums.reduce((a, b) => a + b);
  if (Math.abs(target) > sum || (target + sum) % 2 === 1) {
    return 0;
  }
  const bagSize = (target + sum) / 2;
  const n = nums.length;
  const dp = new Array(bagSize + 1).fill(0);
  dp[0] = 1;
  for (let i = 0; i < n; i++) {
    for (let j = bagSize; j >= nums[i]; j--) {
      dp[j] += dp[j - nums[i]];
    }
  }
  return dp[bagSize];
};
```

# 474. 一和零

```js
/**
 * @param {string[]} strs
 * @param {number} m
 * @param {number} n
 * @return {number}
 */
var findMaxForm = function (strs, m, n) {
  const dp = Array.from({ length: m + 1 }, () => new Array(n + 1).fill(0));
  for (const str of strs) {
    let x = 0;
    let y = 0;
    for (const ch of str) {
      if (ch === "0") {
        x++;
      } else {
        y++;
      }
    }
    for (let i = m; i >= x; i--) {
      for (let j = n; j >= y; j--) {
        dp[i][j] = Math.max(dp[i][j], dp[i - x][j - y] + 1);
      }
    }
  }
  return dp[m][n];
};
```

# 518. 零钱兑换 II

```js
/**
 * @param {number} amount
 * @param {number[]} coins
 * @return {number}
 */
var change = function (amount, coins) {
  const n = coins.length;
  const dp = new Array(amount + 1).fill(0);
  dp[0] = 1;
  for (let i = 0; i < n; i++) {
    for (let j = coins[i]; j <= amount; j++) {
      dp[j] += dp[j - coins[i]];
    }
  }
  return dp[amount];
};
```

# 377. 组合总和 Ⅳ

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var combinationSum4 = function (nums, target) {
  const n = nums.length;
  const dp = new Array(target + 1).fill(0);
  dp[0] = 1;
  for (let j = 0; j <= target; j++) {
    for (let i = 0; i < n; i++) {
      if (j >= nums[i]) {
        dp[j] += dp[j - nums[i]];
      }
    }
  }
  return dp[target];
};
```

# 322. 零钱兑换

```js
/**
 * @param {number[]} coins
 * @param {number} amount
 * @return {number}
 */
var coinChange = function (coins, amount) {
  const n = coins.length;
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  for (let i = 0; i < n; i++) {
    for (let j = coins[i]; j <= amount; j++) {
      dp[j] = Math.min(dp[j], dp[j - coins[i]] + 1);
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
};
```

# 279. 完全平方数

```js
/**
 * @param {number} n
 * @return {number}
 */
var numSquares = function (n) {
  const dp = new Array(n + 1).fill(Infinity);
  dp[0] = 0;
  for (let i = 1; i * i <= n; i++) {
    for (let j = i * i; j <= n; j++) {
      dp[j] = Math.min(dp[j], dp[j - i * i] + 1);
    }
  }
  return dp[n];
};
```

# 139. 单词拆分

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {boolean}
 */
var wordBreak = function (s, wordDict) {
  const n = s.length;
  const dp = new Array(n + 1).fill(false);
  dp[0] = true;
  for (let i = 1; i <= n; i++) {
    for (let j = 0; j < i; j++) {
      const word = s.substring(j, i);
      if (wordDict.includes(word) && dp[j]) {
        dp[i] = true;
      }
    }
  }
  return dp[n];
};
```

# 198. 打家劫舍

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
  const n = nums.length;
  const dp = new Array(n).fill(0);
  dp[0] = nums[0];
  dp[1] = Math.max(nums[0], nums[1]);
  for (let i = 2; i < n; i++) {
    dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
  }
  return dp[n - 1];
};
```

# 213. 打家劫舍 II

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
  const fn = (nums) => {
    const n = nums.length;
    const dp = new Array(n).fill(0);
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);
    for (let i = 2; i < n; i++) {
      dp[i] = Math.max(dp[i - 1], dp[i - 2] + nums[i]);
    }
    return dp[n - 1];
  };
  const n = nums.length;
  if (n === 0) return 0;
  if (n === 1) return nums[0];
  return Math.max(fn(nums.slice(0, n - 1)), fn(nums.slice(1, n)));
};
```

# 337. 打家劫舍 III

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var rob = function (root) {
  const fn = (cur) => {
    if (cur === null) {
      return [0, 0];
    }

    const left = fn(cur.left);
    const right = fn(cur.right);

    const v1 = Math.max(...left) + Math.max(...right);
    const v2 = cur.val + left[0] + right[0];

    return [v1, v2];
  };

  return Math.max(...fn(root));
};
```

# 121. 买卖股票的最佳时机

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () => new Array(2).fill(0));
  dp[0][0] = -prices[0];
  dp[0][1] = 0;
  for (let i = 1; i < n; i++) {
    dp[i][0] = Math.max(dp[i - 1][0], -prices[i]);
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
  }
  return Math.max(...dp[n - 1]);
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
  const dp = Array.from({ length: n }, () => new Array(2).fill(0));
  dp[0][0] = -prices[0];
  dp[0][1] = 0;
  for (let i = 1; i < n; i++) {
    dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
  }
  return Math.max(...dp[n - 1]);
};
```

# 123. 买卖股票的最佳时机 III

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () => new Array(5).fill(0));
  dp[0] = [0, -prices[0], 0, -prices[0], 0];
  for (let i = 1; i < n; i++) {
    dp[i][0] = dp[i - 1][0];
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
    dp[i][2] = Math.max(dp[i - 1][2], dp[i - 1][1] + prices[i]);
    dp[i][3] = Math.max(dp[i - 1][3], dp[i - 1][2] - prices[i]);
    dp[i][4] = Math.max(dp[i - 1][4], dp[i - 1][3] + prices[i]);
  }
  return Math.max(...dp[n - 1]);
};
```

# 188. 买卖股票的最佳时机 IV

```js
/**
 * @param {number} k
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (k, prices) {
  const n = prices.length;
  const m = 2 * k + 1;
  const dp = Array.from({ length: n }, () => new Array(m).fill(0));
  for (let j = 1; j < m; j += 2) {
    dp[0][j] = -prices[0];
  }
  for (let i = 1; i < n; i++) {
    for (let j = 1; j < m; j++) {
      dp[i][j] = Math.max(
        dp[i - 1][j],
        dp[i - 1][j - 1] + (j % 2 === 0 ? prices[i] : -prices[i])
      );
    }
  }
  return Math.max(...dp[n - 1]);
};
```

# 309. 买卖股票的最佳时机含冷冻期

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  const n = prices.length;
  // 0：持股 1：保持卖出股 2：卖出股 3：冷冻期
  const dp = Array.from({ length: n }, () => new Array(4).fill(0));
  dp[0] = [-prices[0], 0, 0, 0];
  for (let i = 1; i < n; i++) {
    dp[i][0] = Math.max(
      dp[i - 1][0],
      dp[i - 1][1] - prices[i],
      dp[i - 1][3] - prices[i]
    );
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][3]);
    dp[i][2] = dp[i - 1][0] + prices[i];
    dp[i][3] = dp[i - 1][2];
  }
  return Math.max(...dp[n - 1]);
};
```

# 714. 买卖股票的最佳时机含手续费

```js
/**
 * @param {number[]} prices
 * @param {number} fee
 * @return {number}
 */
var maxProfit = function (prices, fee) {
  const n = prices.length;
  const dp = Array.from({ length: n }, () => new Array(2).fill(0));
  dp[0][0] = -prices[0];
  dp[0][1] = 0;
  for (let i = 1; i < n; i++) {
    dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
    dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] + prices[i] - fee);
  }
  return Math.max(...dp[n - 1]);
};
```

# 300. 最长递增子序列

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var lengthOfLIS = function (nums) {
  const n = nums.length;
  const dp = new Array(n).fill(1);
  for (let i = 1; i < n; i++) {
    for (let j = 0; j < i; j++) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }
  return Math.max(...dp);
};
```

# 674. 最长连续递增序列

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findLengthOfLCIS = function (nums) {
  const n = nums.length;
  const dp = new Array(n).fill(1);
  for (let i = 1; i < n; i++) {
    for (let j = i - 1; j >= 0 && nums[j + 1] > nums[j]; j--) {
      if (nums[i] > nums[j]) {
        dp[i] = Math.max(dp[i], dp[j] + 1);
      }
    }
  }
  return Math.max(...dp);
};
```

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findLengthOfLCIS = function (nums) {
  const n = nums.length;
  const dp = new Array(n).fill(1);
  for (let i = 1; i < n; i++) {
    if (nums[i] > nums[i - 1]) {
      dp[i] = dp[i - 1] + 1;
    }
  }
  return Math.max(...dp);
};
```

# 718. 最长重复子数组

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findLength = function (nums1, nums2) {
  const n = nums1.length;
  const m = nums2.length;
  const dp = Array.from({ length: n + 1 }, () => new Array(m + 1).fill(0));
  let ans = 0;
  for (let i = 1; i <= n; i++) {
    for (let j = 1; j <= m; j++) {
      if (nums1[i - 1] === nums2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
        ans = Math.max(ans, dp[i][j]);
      }
    }
  }
  return ans;
};
```