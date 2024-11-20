# 77. 组合

```js
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function (n, k) {
  const ans = [];
  const path = [];
  const dfs = (start) => {
    if (path.length === k) {
      ans.push([...path]);
      return;
    }
    for (let i = start; i <= n; i++) {
      path.push(i);
      dfs(i + 1);
      path.pop();
    }
  };
  dfs(1);
  return ans;
};
```

```js
/**
 * @param {number} n
 * @param {number} k
 * @return {number[][]}
 */
var combine = function (n, k) {
  const ans = [];
  const path = [];
  const dfs = (start) => {
    if (path.length === k) {
      ans.push([...path]);
      return;
    }
    for (let i = start; i <= n - (k - path.length) + 1; i++) {
      path.push(i);
      dfs(i + 1);
      path.pop();
    }
  };
  dfs(1);
  return ans;
};
```

# 216. 组合总和 III

```js
/**
 * @param {number} k
 * @param {number} n
 * @return {number[][]}
 */
var combinationSum3 = function (k, n) {
  const path = [];
  const ans = [];
  const dfs = (start, sum) => {
    if (sum > n) {
      return;
    }
    if (path.length === k) {
      if (sum === n) {
        ans.push([...path]);
      }
      return;
    }
    for (let i = start; i <= 9; i++) {
      path.push(i);
      dfs(i + 1, sum + i);
      path.pop();
    }
  };
  dfs(1, 0);
  return ans;
};
```