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