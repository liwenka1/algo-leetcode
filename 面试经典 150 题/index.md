# 169. 多数元素

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function (nums) {
  const n = nums.length;
  const k = n / 2;
  const map = new Map();
  for (const num of nums) {
    map.set(num, (map.get(num) || 0) + 1);
    if (map.get(num) > k) {
      return num;
    }
  }
};
```