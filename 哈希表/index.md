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

# 349. 两个数组的交集

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersection = function (nums1, nums2) {
  const set1 = new Set(nums1);
  const set2 = new Set(nums2);
  const ans = new Set();
  for (const num of set2) {
    if (set1.has(num)) {
      ans.add(num);
    }
  }
  return Array.from(ans);
};
```