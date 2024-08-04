# 3111. 覆盖所有点的最少矩形数目

```js
/**
 * @param {number[][]} points
 * @param {number} w
 * @return {number}
 */
var minRectanglesToCoverPoints = function (points, w) {
  points.sort((a, b) => a[0] - b[0]);
  let ans = 0;
  let end = -1;
  for (const [x, _] of points) {
    if (x > end) {
      ans++;
      end = x + w;
    }
  }
  return ans;
};
```