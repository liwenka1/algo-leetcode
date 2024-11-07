# 344. 反转字符串

```js
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseString = function (s) {
  const n = s.length;
  for (let i = 0; i < n / 2; i++) {
    [s[i], s[n - 1 - i]] = [s[n - 1 - i], s[i]];
  }
};
```

# 541. 反转字符串 II

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function (s, k) {
  const reverseString = function (s) {
    s = s.split("");
    const n = s.length;
    for (let i = 0; i < n / 2; i++) {
      [s[i], s[n - 1 - i]] = [s[n - 1 - i], s[i]];
    }
    return s.join("");
  };
  const n = s.length;
  let ans = "";
  for (let i = 0; i < n; i += 2 * k) {
    ans += reverseString(s.substring(i, i + k)) + s.substring(i + k, i + 2 * k);
  }
  return ans;
};
```

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function (s, k) {
  const n = s.length;
  let ans = "";
  for (let i = 0; i < n; i += 2 * k) {
    ans +=
      s
        .substring(i, i + k)
        .split("")
        .reverse()
        .join("") + s.substring(i + k, i + 2 * k);
  }
  return ans;
};
```