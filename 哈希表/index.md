# 242. 有效的字母异位词

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function (s, t) {
  const n = s.length;
  const m = t.length;
  if (n !== m) {
    return false;
  }
  const cnt = new Array(26).fill(0);
  for (let i = 0; i < n; i++) {
    cnt[s[i].charCodeAt(0) - "a".charCodeAt(0)]++;
    cnt[t[i].charCodeAt(0) - "a".charCodeAt(0)]--;
  }
  return cnt.every((i) => i === 0);
};
```