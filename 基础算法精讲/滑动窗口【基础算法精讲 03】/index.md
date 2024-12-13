# 209. 长度最小的子数组

```js
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function (target, nums) {
  const n = nums.length;
  let sum = 0;
  let ans = Infinity;
  for (let left = 0, right = 0; right < n; right++) {
    sum += nums[right];
    while (sum >= target) {
      console.log(right, left);
      ans = Math.min(ans, right - left + 1);
      sum -= nums[left];
      left++;
    }
  }
  return ans === Infinity ? 0 : ans;
};
```