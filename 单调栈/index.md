# 739. 每日温度

```js
/**
 * @param {number[]} temperatures
 * @return {number[]}
 */
var dailyTemperatures = function (temperatures) {
  const n = temperatures.length;
  const stack = [0];
  const ans = new Array(n).fill(0);
  for (let i = 1; i < n; i++) {
    while (
      stack.length &&
      temperatures[i] > temperatures[stack[stack.length - 1]]
    ) {
      const j = stack.pop();
      ans[j] = i - j;
    }
    stack.push(i);
  }
  return ans;
};
```