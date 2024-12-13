# 167. 两数之和 II - 输入有序数组

```js
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (numbers, target) {
  const n = numbers.length;
  let left = 0;
  let right = n - 1;
  while (left < right) {
    const sum = numbers[left] + numbers[right];
    if (sum > target) {
      right--;
    } else if (sum < target) {
      left++;
    } else {
      return [left + 1, right + 1];
    }
  }
};
```

# 15. 三数之和

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function (nums) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const ans = [];
  for (let i = 0; i < n - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) {
      continue;
    }
    if (nums[i] + nums[n - 2] + nums[n - 1] < 0) {
      continue;
    }
    if (nums[i] + nums[i + 1] + nums[i + 2] > 0) {
      break;
    }
    let left = i + 1;
    let right = n - 1;
    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];
      if (sum > 0) {
        while (nums[right] === nums[right - 1]) {
          right--;
        }
        right--;
      } else if (sum < 0) {
        while (nums[left] === nums[left + 1]) {
          left++;
        }
        left++;
      } else {
        ans.push([nums[i], nums[left], nums[right]]);
        while (nums[right] === nums[right - 1]) {
          right--;
        }
        right--;
        while (nums[left] === nums[left + 1]) {
          left++;
        }
        left++;
      }
    }
  }
  return ans;
};
```

# 2824. 统计和小于目标的下标对数目

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var countPairs = function (nums, target) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  let left = 0;
  let right = n - 1;
  let ans = 0;
  while (left < right) {
    const sum = nums[left] + nums[right];
    if (sum >= target) {
      right--;
    } else {
      ans += right - left;
      left++;
    }
  }
  return ans;
};
```

# 16. 最接近的三数之和

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function (nums, target) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  let ans1 = Infinity;
  let ans2 = -Infinity;
  for (let i = 0; i < n - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) {
      continue;
    }
    let left = i + 1;
    let right = n - 1;
    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right] - target;
      if (sum > 0) {
        ans1 = Math.min(ans1, sum);
        while (nums[right] === nums[right - 1]) {
          right--;
        }
        right--;
      } else if (sum < 0) {
        ans2 = Math.max(ans2, sum);
        while (nums[left] === nums[left + 1]) {
          left++;
        }
        left++;
      } else {
        return target;
      }
    }
  }
  return ans1 > -ans2 ? ans2 + target : ans1 + target;
};
```

# 18. 四数之和

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[][]}
 */
var fourSum = function (nums, target) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  const ans = [];
  for (let i = 0; i < n - 3; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) {
      continue;
    }
    if (nums[i] + nums[n - 3] + nums[n - 2] + nums[n - 1] < target) {
      continue;
    }
    if (nums[i] + nums[i + 1] + nums[i + 2] + nums[i + 3] > target) {
      break;
    }
    for (let j = i + 1; j < n - 2; j++) {
      if (j > i + 1 && nums[j] === nums[j - 1]) {
        continue;
      }
      if (nums[i] + nums[j] + nums[n - 2] + nums[n - 1] < target) {
        continue;
      }
      if (nums[i] + nums[j] + nums[j + 1] + nums[j + 2] > target) {
        break;
      }
      let left = j + 1;
      let right = n - 1;
      while (left < right) {
        const sum = nums[i] + nums[j] + nums[left] + nums[right];
        if (sum > target) {
          while (nums[right] === nums[right - 1]) {
            right--;
          }
          right--;
        } else if (sum < target) {
          while (nums[left] === nums[left + 1]) {
            left++;
          }
          left++;
        } else {
          ans.push([nums[i], nums[j], nums[left], nums[right]]);
          while (nums[right] === nums[right - 1]) {
            right--;
          }
          right--;
          while (nums[left] === nums[left + 1]) {
            left++;
          }
          left++;
        }
      }
    }
  }
  return ans;
};
```

# 611. 有效三角形的个数

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var triangleNumber = function (nums) {
  nums.sort((a, b) => a - b);
  const n = nums.length;
  let ans = 0;
  for (let i = 2; i < n; i++) {
    let left = 0;
    let right = i - 1;
    while (left < right) {
      const sum = nums[left] + nums[right];
      if (sum > nums[i]) {
        ans += right - left;
        right--;
      } else {
        left++;
      }
    }
  }
  return ans;
};
```

# 11. 盛最多水的容器

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function (height) {
  const n = height.length;
  let left = 0;
  let right = n - 1;
  let ans = 0;
  while (left < right) {
    if (height[left] > height[right]) {
      ans = Math.max(ans, (right - left) * height[right]);
      right--;
    } else {
      ans = Math.max(ans, (right - left) * height[left]);
      left++;
    }
  }
  return ans;
};
```