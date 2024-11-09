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