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

# 1. 两数之和

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  const map = new Map();
  const n = nums.length;
  for (let i = 0; i < n; i++) {
    map.set(target - nums[i], i);
  }
  for (let i = 0; i < n; i++) {
    if (map.has(nums[i]) && i !== map.get(nums[i])) {
      return [i, map.get(nums[i])];
    }
  }
};
```

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  const map = new Map();
  const n = nums.length;
  for (let i = 0; i < n; i++) {
    const s = target - nums[i];
    if (map.has(s)) {
      return [i, map.get(s)];
    }
    map.set(nums[i], i);
  }
};
```

# 454. 四数相加 II

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number[]} nums3
 * @param {number[]} nums4
 * @return {number}
 */
var fourSumCount = function (nums1, nums2, nums3, nums4) {
  const map = new Map();
  for (const num1 of nums1) {
    for (const num2 of nums2) {
      const sum = num1 + num2;
      map.set(sum, (map.get(sum) || 0) + 1);
    }
  }
  let ans = 0;
  for (const num3 of nums3) {
    for (const num4 of nums4) {
      const sum = num3 + num4;
      if (map.has(-sum)) {
        ans += map.get(-sum);
      }
    }
  }
  return ans;
};
```