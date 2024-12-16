# 547. 省份数量

```js
/**
 * @param {number[][]} isConnected
 * @return {number}
 */
var findCircleNum = function (isConnected) {
  const visited = new Set();
  const n = isConnected.length;

  const dfs = (i) => {
    for (let j = 0; j < n; j++) {
      if (isConnected[i][j] === 1 && !visited.has(j)) {
        visited.add(j);
        dfs(j);
      }
    }
  };

  let ans = 0;
  for (let i = 0; i < n; i++) {
    if (!visited.has(i)) {
      dfs(i);
      ans++;
    }
  }
  return ans;
};
```

# 1971. 寻找图中是否存在路径

```js
/**
 * @param {number} n
 * @param {number[][]} edges
 * @param {number} source
 * @param {number} destination
 * @return {boolean}
 */
var validPath = function (n, edges, source, destination) {
  const map = new Map();

  for (const [u, v] of edges) {
    if (!map.has(u)) {
      map.set(u, []);
    }
    if (!map.has(v)) {
      map.set(v, []);
    }
    map.get(u).push(v);
    map.get(v).push(u);
  }

  const visited = new Set();

  const dfs = (source) => {
    if (source === destination) {
      return true;
    }
    visited.add(source);
    for (const v of map.get(source) || []) {
      if (!visited.has(v) && dfs(v)) {
        return true;
      }
    }
    return false;
  };

  return dfs(source);
};
```