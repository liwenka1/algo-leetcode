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

# 151. 反转字符串中的单词

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function (s) {
  s = Array.from(s);
  const n = s.length;
  let slow = 0;
  for (let fast = 0; fast < n; fast++) {
    if (s[fast] !== " ") {
      if (slow !== 0) {
        s[slow++] = " ";
      }
      while (fast < n && s[fast] !== " ") {
        s[slow++] = s[fast++];
      }
    }
  }
  return s.join("").slice(0, slow).split(" ").reverse().join(" ");
};
```

# 459. 重复的子字符串

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var repeatedSubstringPattern = function (s) {
  const ss = s + s;
  const n = ss.length;
  return ss.substring(1, n - 1).includes(s);
};
```