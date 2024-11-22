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

# 17. 电话号码的字母组合

```js
/**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function (digits) {
  const n = digits.length;
  if (n === 0) {
    return [];
  }
  const list = {
    2: "abc",
    3: "def",
    4: "ghi",
    5: "jkl",
    6: "mno",
    7: "pqrs",
    8: "tuv",
    9: "wxyz",
  };
  const path = [];
  const ans = [];
  const dfs = (start) => {
    if (start === n) {
      ans.push(path.join(""));
      return;
    }
    const strList = list[digits[start]];
    for (const str of strList) {
      path.push(str);
      dfs(start + 1);
      path.pop();
    }
  };
  dfs(0);
  return ans;
};
```

# 39. 组合总和

```js
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (candidates, target) {
  const n = candidates.length;
  const path = [];
  const ans = [];
  const dfs = (start, sum) => {
    if (sum === target) {
      ans.push([...path]);
      return;
    }
    if (start === n || sum > target) {
      return;
    }
    for (let i = start; i < n; i++) {
      path.push(candidates[i]);
      dfs(i, sum + candidates[i]);
      path.pop();
    }
  };
  dfs(0, 0);
  return ans;
};
```

# 40. 组合总和 II

```js
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum2 = function (candidates, target) {
  candidates.sort((a, b) => a - b);
  const n = candidates.length;
  const path = [];
  const ans = [];
  const dfs = (start, sum) => {
    if (sum === target) {
      ans.push([...path]);
      return;
    }
    if (start === n || sum > target) {
      return;
    }
    for (let i = start; i < n; i++) {
      if (i > start && candidates[i] === candidates[i - 1]) {
        continue;
      }
      path.push(candidates[i]);
      dfs(i + 1, sum + candidates[i]);
      path.pop();
    }
  };
  dfs(0, 0);
  return ans;
};
```