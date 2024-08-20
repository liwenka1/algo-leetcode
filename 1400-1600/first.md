# 3111. 覆盖所有点的最少矩形数目

```js
/**
 * @param {number[][]} points
 * @param {number} w
 * @return {number}
 */
var minRectanglesToCoverPoints = function (points, w) {
  points.sort((a, b) => a[0] - b[0]);
  let ans = 0;
  let end = -1;
  for (const [x, _] of points) {
    if (x > end) {
      ans++;
      end = x + w;
    }
  }
  return ans;
};
```

# 1237. 找出给定方程的正整数解

```js
/**
 * // This is the CustomFunction's API interface.
 * // You should not implement it, or speculate about its implementation
 * function CustomFunction() {
 *     @param {integer, integer} x, y
 *     @return {integer}
 *     this.f = function(x, y) {
 *         ...
 *     };
 * };
 */

/**
 * @param {CustomFunction} customfunction
 * @param {integer} z
 * @return {integer[][]}
 */
var findSolution = function (customfunction, z) {
  let x = 1;
  let y = 1000;
  const ans = [];
  while (x <= 1000 && y >= 1) {
    const res = customfunction.f(x, y);
    if (res > z) {
      y--;
    } else if (res < z) {
      x++;
    } else {
      ans.push([x++, y--]);
    }
  }
  return ans;
};
```

# 3101. 交替子数组计数

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var countAlternatingSubarrays = function (nums) {
  let ans = 1;
  for (let start = 0, end = 1; end < nums.length; end++) {
    if (nums[end] === nums[end - 1]) {
      start = end;
    }
    ans += end - start + 1;
  }
  return ans;
};
```

# 2734. 执行子串操作后的字典序最小字符串

```js
/**
 * @param {string} s
 * @return {string}
 */
var smallestString = function (s) {
  const list = s.split("");
  const n = list.length;
  for (let i = 0; i < n; i++) {
    if (list[i] === "a") continue;
    for (let j = i; j < n && list[j] !== "a"; j++) {
      list[j] = String.fromCharCode(list[j].charCodeAt(0) - 1);
    }
    return list.join("");
  }
  list[n - 1] = "z";
  return list.join("");
};
```

# 2996. 大于等于顺序前缀和的最小缺失整数

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var missingInteger = function (nums) {
  let sum = nums[0];
  const n = nums.length;
  for (let i = 1; i < n, nums[i] === nums[i - 1] + 1; i++) {
    sum += nums[i];
  }
  const set = new Set(nums);
  while (set.has(sum)) {
    sum++;
  }
  return sum;
};
```

# 2946. 循环移位后的矩阵相似检查

```js
/**
 * @param {number[][]} mat
 * @param {number} k
 * @return {boolean}
 */
var areSimilar = function (mat, k) {
    const n = mat[0].length
    k %= n;
    if (k === 0) return true;
    for (const num of mat) {
        for (let i = 0; i < n; i++) {
            if (num[i] !== num[(i + k) % n]) return false;
        }
    }
    return true;
};
```

# 2744. 最大字符串配对数目

```js
/**
 * @param {string[]} words
 * @return {number}
 */
var maximumNumberOfStringPairs = function (words) {
  const set = new Set();
  let ans = 0;
  for (const word of words) {
    if (set.has(word.split("").reverse().join(""))) {
      ans++;
    }
    set.add(word);
  }
  return ans;
};
```

# 2451. 差值数组不同的字符串

```js
/**
 * @param {string[]} words
 * @return {string}
 */
var oddString = function (words) {
  const map = new Map();
  for (const word of words) {
    const keys = word.split("").map((s) => s.charCodeAt(0));
    const n = keys.length;
    const res = [];
    for (let i = 1; i < n; i++) {
      res.push(keys[i] - keys[i - 1]);
    }
    const keyString = res.join(",");
    if (!map.has(keyString)) {
      map.set(keyString, []);
    }
    map.get(keyString).push(word);
  }
  for (const group of map.values()) {
    if (group.length === 1) {
      return group[0];
    }
  }
  return "";
};
```

# 1886. 判断矩阵经轮转后是否一致

```js
/**
 * @param {number[][]} mat
 * @param {number[][]} target
 * @return {boolean}
 */
var findRotation = function (mat, target) {
  const n = mat.length;
  const isEqual = (a, b) => {
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        if (a[i][j] !== b[i][j]) {
          return false;
        }
      }
    }
    return true;
  };
  const rotate = (matrix) => {
    const newMatrix = Array.from({ length: n }, () => Array(n).fill(0));
    for (let i = 0; i < n; i++) {
      for (let j = 0; j < n; j++) {
        newMatrix[j][n - 1 - i] = matrix[i][j];
      }
    }
    return newMatrix;
  };
  for (let k = 0; k < 4; k++) {
    if (isEqual(mat, target)) {
      return true;
    }
    mat = rotate(mat);
  }
  return false;
};
```

# 2110. 股票平滑下跌阶段的数目

```js
/**
 * @param {number[]} prices
 * @return {number}
 */
var getDescentPeriods = function (prices) {
  let ans = 1;
  let prew = 1;
  const n = prices.length;
  for (let i = 1; i < n; i++) {
    if (prices[i - 1] - prices[i] === 1) {
      prew++;
    } else {
      prew = 1;
    }
    ans += prew;
  }
  return ans;
};
```

# 2834. 找出美丽数组的最小和

```js
/**
 * @param {number} n
 * @param {number} target
 * @return {number}
 */
var minimumPossibleSum = function (n, target) {
  const mod = BigInt(1000000007);
  const nBig = BigInt(n);
  const targetBig = BigInt(target);
  const m = targetBig / 2n;

  if (nBig <= m) {
    return Number((((1n + nBig) * nBig) / 2n) % mod);
  }

  const sum1 = ((1n + m) * m) / 2n;
  const sum2 = ((targetBig * 2n + nBig - m - 1n) * (nBig - m)) / 2n;

  return Number((sum1 + sum2) % mod);
};
```

# 1138. 字母板上的路径

```js
/**
 * @param {string} target
 * @return {string}
 */
var alphabetBoardPath = function (target) {
  let x = 0;
  let y = 0;
  const ans = [];
  for (const s of target) {
    const n = s.charCodeAt(0) - "a".charCodeAt(0);
    const nx = n % 5;
    const ny = Math.floor(n / 5);
    const v = nx > x ? "R".repeat(nx - x) : "L".repeat(x - nx);
    const h = ny > y ? "D".repeat(ny - y) : "U".repeat(y - ny);
    x = nx;
    y = ny;
    ans.push(s === "z" ? v + h + "!" : h + v + "!");
  }
  return ans.join("");
};
```

# 3121. 统计特殊字母的数量 II

```js
/**
 * @param {string} word
 * @return {number}
 */
var numberOfSpecialChars = function (word) {
  const ans = new Set(),
    delSet = new Set(),
    upSet = new Set(),
    lowSet = new Set();
  word = word.split("");
  for (const s of word) {
    if (s === s.toUpperCase()) {
      if (lowSet.has(s.toLowerCase())) {
        ans.add(s);
      }
      upSet.add(s);
    } else {
      if (upSet.has(s.toUpperCase())) {
        if (lowSet.has(s)) {
          delSet.add(s);
        }
      } else {
        lowSet.add(s);
      }
    }
  }
  return ans.size - delSet.size;
};
```

# 2521. 数组乘积中的不同质因数数目

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var distinctPrimeFactors = function (nums) {
  const ans = new Set();
  for (const num of nums) {
    let i = 2;
    let x = num;
    while (i * i <= x) {
      if (x % i === 0) {
        ans.add(i);
        while (x % i === 0) {
          x /= i;
        }
      }
      i++;
    }
    if (x > 1) ans.add(x);
  }
  return ans.size;
};
```

# 2383. 赢得比赛需要的最少训练时长

```js
/**
 * @param {number} initialEnergy
 * @param {number} initialExperience
 * @param {number[]} energy
 * @param {number[]} experience
 * @return {number}
 */
var minNumberOfHours = function (
  initialEnergy,
  initialExperience,
  energy,
  experience
) {
  const energySum = energy.reduce((a, b) => a + b);
  let requiredEnergy = Math.max(0, energySum - initialEnergy + 1);
  let requiredExperience = 0;
  for (const e of experience) {
    if (initialExperience <= e) {
      requiredExperience += e + 1 - initialExperience;
      initialExperience = e + 1;
    }
    initialExperience += e;
  }
  return requiredEnergy + requiredExperience;
};
```

# 1985. 找出数组中的第 K 大整数

```js
/**
 * @param {string[]} nums
 * @param {number} k
 * @return {string}
 */
var kthLargestNumber = function (nums, k) {
  const newNums = nums.map((i) => BigInt(i));
  newNums.sort((a, b) => {
    if (a > b) return -1;
    if (a < b) return 1;
    return 0;
  });
  return newNums[k - 1].toString();
};
```

# 2825. 循环增长使字符串子序列等于另一个字符串

```js
/**
 * @param {string} str1
 * @param {string} str2
 * @return {boolean}
 */
var canMakeSubsequence = function (str1, str2) {
  if (str1.length < str2.length) return false;
  let i = 0;
  for (const s of str1) {
    const c = s === "z" ? "a" : String.fromCharCode(s.charCodeAt(0) + 1);
    if (s === str2[i] || c === str2[i]) {
      i++;
      if (i === str2.length) return true;
    }
  }
  return false;
};
```