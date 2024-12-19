# 34. 在排序数组中查找元素的第一个和最后一个位置

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function (nums, target) {
  const n = nums.length;
  const lowerBound = (target) => {
    let left = 0;
    let right = n - 1;
    while (left <= right) {
      const mid = Math.floor((left + right) / 2);
      if (nums[mid] < target) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
    return left;
  };
  const ansleft = lowerBound(target);
  const ansright = lowerBound(target + 1) - 1;
  return nums[ansleft] === target && nums[ansright] === target
    ? [ansleft, ansright]
    : [-1, -1];
};
```