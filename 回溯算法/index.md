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

# 131. 分割回文串

```js
/**
 * @param {string} s
 * @return {string[][]}
 */
var partition = function (s) {
  const n = s.length;
  const path = [];
  const ans = [];
  const isPalindrome = (str) => {
    let left = 0;
    let right = str.length - 1;
    while (left < right) {
      if (str[left] !== str[right]) return false;
      left++;
      right--;
    }
    return true;
  };
  const dfs = (start) => {
    if (start === n) {
      ans.push([...path]);
      return;
    }
    for (let i = start; i < n; i++) {
      const str = s.substring(start, i + 1);
      if (isPalindrome(str)) {
        path.push(str);
        dfs(i + 1);
        path.pop();
      }
    }
  };
  dfs(0);
  return ans;
};
```

# 93. 复原 IP 地址

```js
/**
 * @param {string} s
 * @return {string[]}
 */
var restoreIpAddresses = function (s) {
  const n = s.length;
  const path = [];
  const ans = [];
  const dfs = (start, cnt) => {
    if (cnt === 0) {
      if (start === n) {
        ans.push(path.join("."));
      }
      return;
    }
    for (let i = start; i < n; i++) {
      const str = s.substring(start, i + 1);
      if ((str.length === 1 || str[0] !== "0") && Number(str) <= 255) {
        path.push(str);
        dfs(i + 1, cnt - 1);
        path.pop();
      }
    }
  };
  dfs(0, 4);
  return ans;
};
```

# 78. 子集

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function (nums) {
  const n = nums.length;
  const path = [];
  const ans = [];
  const dfs = (start) => {
    ans.push([...path]);
    if (start === n) {
      return;
    }
    for (let i = start; i < n; i++) {
      path.push(nums[i]);
      dfs(i + 1);
      path.pop();
    }
  };
  dfs(0);
  return ans;
};
```

# 90. 子集 II

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function (nums) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const path = [];
  const ans = [];
  const dfs = (start) => {
    ans.push([...path]);
    if (start === n) {
      return;
    }
    for (let i = start; i < n; i++) {
      if (i > start && nums[i] === nums[i - 1]) {
        continue;
      }
      path.push(nums[i]);
      dfs(i + 1);
      path.pop();
    }
  };
  dfs(0);
  return ans;
};
```

# 491. 非递减子序列

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var findSubsequences = function (nums) {
  const n = nums.length;
  const path = [];
  const ans = [];
  const dfs = (start) => {
    if (path.length >= 2) {
      ans.push([...path]);
    }
    if (start === n) {
      return;
    }
    const set = new Set();
    for (let i = start; i < n; i++) {
      if (nums[i] < path[path.length - 1] || set.has(nums[i])) {
        continue;
      }
      set.add(nums[i]);
      path.push(nums[i]);
      dfs(i + 1);
      path.pop();
    }
  };
  dfs(0);
  return ans;
};
```

# 46. 全排列

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permute = function (nums) {
  const n = nums.length;
  const used = new Array(n).fill(false);
  const path = [];
  const ans = [];
  const dfs = () => {
    if (path.length === n) {
      ans.push([...path]);
      return;
    }
    for (let i = 0; i < n; i++) {
      if (used[i]) {
        continue;
      }
      used[i] = true;
      path.push(nums[i]);
      dfs();
      path.pop();
      used[i] = false;
    }
  };
  dfs();
  return ans;
};
```

# 47. 全排列 II

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function (nums) {
  const n = nums.length;
  const used = new Array(n).fill(false);
  const path = [];
  const ans = [];
  const dfs = () => {
    if (path.length === n) {
      ans.push([...path]);
      return;
    }
    const set = new Set();
    for (let i = 0; i < n; i++) {
      if (used[i] || set.has(nums[i])) {
        continue;
      }
      set.add(nums[i]);
      used[i] = true;
      path.push(nums[i]);
      dfs();
      path.pop();
      used[i] = false;
    }
  };
  dfs();
  return ans;
};
```

# 51. N 皇后

```js
/**
 * @param {number} n
 * @return {string[][]}
 */
var solveNQueens = function (n) {
  const path = Array.from({ length: n }, () => new Array(n).fill("."));
  const cols = new Set();
  const diag1 = new Set();
  const diag2 = new Set();
  const ans = [];
  const dfs = (row) => {
    if (row === n) {
      ans.push(path.map((row) => row.join("")));
      return;
    }
    for (let i = 0; i < n; i++) {
      if (cols.has(i) || diag1.has(row - i) || diag2.has(row + i)) {
        continue;
      }
      path[row][i] = "Q";
      cols.add(i);
      diag1.add(row - i);
      diag2.add(row + i);

      dfs(row + 1);

      path[row][i] = ".";
      cols.delete(i);
      diag1.delete(row - i);
      diag2.delete(row + i);
    }
  };
  dfs(0);
  return ans;
};
```