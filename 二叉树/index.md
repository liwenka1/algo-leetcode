# 144. 二叉树的前序遍历

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var preorderTraversal = function (root) {
  const ans = [];
  const preorder = (cur) => {
    if (cur === null) {
      return;
    }
    ans.push(cur.val);
    preorder(cur.left);
    preorder(cur.right);
  };
  preorder(root);
  return ans;
};
```

# 145. 二叉树的后序遍历

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var postorderTraversal = function (root) {
  const ans = [];
  const postorder = (cur) => {
    if (cur === null) {
      return;
    }
    postorder(cur.left);
    postorder(cur.right);
    ans.push(cur.val);
  };
  postorder(root);
  return ans;
};
```

# 94. 二叉树的中序遍历

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var inorderTraversal = function (root) {
  const ans = [];
  const inorder = (cur) => {
    if (cur === null) {
      return;
    }
    inorder(cur.left);
    ans.push(cur.val);
    inorder(cur.right);
  };
  inorder(root);
  return ans;
};
```

# 102. 二叉树的层序遍历

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function (root) {
  if (root === null) {
    return [];
  }
  const queue = [root];
  const ans = [];
  while (queue.length) {
    let size = queue.length;
    const vals = [];
    while (size > 0) {
      const node = queue.shift();
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
      vals.push(node.val);
      size--;
    }
    ans.push(vals);
  }
  return ans;
};
```

# 226. 翻转二叉树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var invertTree = function (root) {
  const invert = (node) => {
    if (node === null) {
      return;
    }
    [node.left, node.right] = [node.right, node.left];
    invert(node.left);
    invert(node.right);
  };
  invert(root);
  return root;
};
```

# 101. 对称二叉树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isSymmetric = function (root) {
  const dfs = (left, right) => {
    if (left === null || right === null) {
      return left === right;
    }
    if (left.val === right.val) {
      return dfs(left.left, right.right) && dfs(right.left, left.right);
    } else {
      return false;
    }
  };
  return dfs(root.left, root.right);
};
```

# 104. 二叉树的最大深度

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function (root) {
  let ans = 0;
  const dfs = (node, depth) => {
    if (node === null) {
      return;
    }
    if (node.left) {
      dfs(node.left, depth + 1);
    }
    if (node.right) {
      dfs(node.right, depth + 1);
    }
    ans = Math.max(ans, depth + 1);
  };
  dfs(root, 0);
  return ans;
};
```

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function (root) {
  if (root === null) {
    return 0;
  }
  const left = maxDepth(root.left);
  const right = maxDepth(root.right);
  return Math.max(left, right) + 1;
};
```

# 111. 二叉树的最小深度

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var minDepth = function (root) {
  if (root === null) {
    return 0;
  }
  const left = minDepth(root.left);
  const right = minDepth(root.right);
  if (root.left === null && root.right) {
    return right + 1;
  }
  if (root.right === null && root.left) {
    return left + 1;
  }
  return Math.min(left, right) + 1;
};
```

# 222. 完全二叉树的节点个数

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var countNodes = function (root) {
  if (root === null) {
    return 0;
  }
  const left = countNodes(root.left);
  const right = countNodes(root.right);
  return left + right + 1;
};
```

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var countNodes = function (root) {
  if (root === null) {
    return 0;
  }
  let leftdepth = 1;
  let rightdepth = 1;
  let left = root.left;
  let right = root.right;
  while (left) {
    left = left.left;
    leftdepth++;
  }
  while (right) {
    right = right.right;
    rightdepth++;
  }
  if (leftdepth === rightdepth) {
    return Math.pow(2, leftdepth) - 1;
  }
  return countNodes(root.left) + countNodes(root.right) + 1;
};
```

# 110. 平衡二叉树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isBalanced = function (root) {
  const dfs = (node) => {
    if (node === null) {
      return 0;
    }
    const left = dfs(node.left);
    if (left === -1) {
      return -1;
    }
    const right = dfs(node.right);
    if (right === -1) {
      return -1;
    }
    return Math.abs(left - right) > 1 ? -1 : Math.max(left, right) + 1;
  };
  return dfs(root) !== -1;
};
```

# 257. 二叉树的所有路径

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {string[]}
 */
var binaryTreePaths = function (root) {
  const ans = [];
  const dfs = (node, path) => {
    if (node === null) {
      return;
    }
    path.push(node.val);
    if (node.left === null && node.right === null) {
      ans.push(path.join("->"));
    }
    dfs(node.left, path);
    dfs(node.right, path);
    path.pop();
  };
  dfs(root, []);
  return ans;
};
```

# 404. 左叶子之和

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var sumOfLeftLeaves = function (root) {
  if (root == null) {
    return 0;
  }
  if (root.left === null && root.right === null) {
    return 0;
  }
  let leftsum;
  if (
    root.left !== null &&
    root.left.left === null &&
    root.left.right === null
  ) {
    leftsum = root.left.val;
  } else {
    leftsum = sumOfLeftLeaves(root.left);
  }
  let rightsum = sumOfLeftLeaves(root.right);
  return leftsum + rightsum;
};
```

# 513. 找树左下角的值

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var findBottomLeftValue = function (root) {
  let maxDepth = -Infinity;
  let ans = 0;
  const dfs = (node, depth) => {
    if (node.left === null && node.right === null) {
      if (depth > maxDepth) {
        maxDepth = depth;
        ans = node.val;
      }
    }
    if (node.left) {
      depth++;
      dfs(node.left, depth);
      depth--;
    }
    if (node.right) {
      depth++;
      dfs(node.right, depth);
      depth--;
    }
  };
  dfs(root, 0);
  return ans;
};
```

# 112. 路径总和

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function (root, targetSum) {
  const dfs = (node, sum) => {
    if (node === null) {
      return false;
    }
    sum += node.val;
    if (node.left === null && node.right === null) {
      return sum === targetSum;
    }
    if (node.left) {
      if (dfs(node.left, sum)) {
        return true;
      }
    }
    if (node.right) {
      if (dfs(node.right, sum)) {
        return true;
      }
    }
    return false;
  };
  return dfs(root, 0);
};
```

# 106. 从中序与后序遍历序列构造二叉树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function (inorder, postorder) {
  const n = postorder.length;
  if (n === 0) {
    return null;
  }
  const rootval = postorder[postorder.length - 1];
  const leftsize = inorder.indexOf(rootval);
  const inorderleft = inorder.slice(0, leftsize);
  const inorderright = inorder.slice(leftsize + 1, n);
  const postorderleft = postorder.slice(0, leftsize);
  const postorderright = postorder.slice(leftsize, n - 1);
  const left = buildTree(inorderleft, postorderleft);
  const right = buildTree(inorderright, postorderright);
  return new TreeNode(rootval, left, right);
};
```

# 654. 最大二叉树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var constructMaximumBinaryTree = function (nums) {
  const n = nums.length;
  if (n === 0) {
    return;
  }
  let maxval = -1;
  let maxindex = -1;
  for (let i = 0; i < n; i++) {
    if (nums[i] > maxval) {
      maxval = nums[i];
      maxindex = i;
    }
  }
  const left = constructMaximumBinaryTree(nums.slice(0, maxindex));
  const right = constructMaximumBinaryTree(nums.slice(maxindex + 1, n));
  return new TreeNode(maxval, left, right);
};
```

# 617. 合并二叉树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @return {TreeNode}
 */
var mergeTrees = function (root1, root2) {
  if (root1 === null && root2 === null) {
    return null;
  }
  const val = (root1?.val || 0) + (root2?.val || 0);
  const left = mergeTrees(root1?.left || null, root2?.left || null);
  const right = mergeTrees(root1?.right || null, root2?.right || null);
  return new TreeNode(val, left, right);
};
```

# 700. 二叉搜索树中的搜索

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */
var searchBST = function (root, val) {
  if (root === null) {
    return null;
  }
  if (root.val === val) {
    return new TreeNode(root.val, root.left, root.right);
  }
  if (root.val < val) {
    return searchBST(root.right, val);
  } else {
    return searchBST(root.left, val);
  }
};
```

# 98. 验证二叉搜索树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isValidBST = function (root) {
  const dfs = (node, min, max) => {
    if (node === null) {
      return true;
    }
    if (min >= node.val || max <= node.val) {
      return false;
    }
    return dfs(node.left, min, node.val) && dfs(node.right, node.val, max);
  };
  return dfs(root, -Infinity, Infinity);
};
```

# 530. 二叉搜索树的最小绝对差

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var getMinimumDifference = function (root) {
  let pre = null;
  let ans = Infinity;
  const dfs = (node) => {
    if (node === null) {
      return;
    }
    dfs(node.left);
    if (pre !== null) {
      ans = Math.min(ans, Math.abs(pre.val - node.val));
    }
    pre = node;
    dfs(node.right);
  };
  dfs(root);
  return ans;
};
```

# 501. 二叉搜索树中的众数

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number[]}
 */
var findMode = function (root) {
  const map = {};
  const dfs = (node) => {
    if (node === null) {
      return;
    }
    if (!map[node.val]) {
      map[node.val] = 0;
    }
    map[node.val]++;
    dfs(node.left);
    dfs(node.right);
  };
  dfs(root);
  const max = Math.max(...Object.values(map));
  return Object.keys(map)
    .filter((key) => map[key] === max)
    .map(Number);
};
```

# 236. 二叉树的最近公共祖先

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function (root, p, q) {
  if (root === null || root === p || root === q) {
    return root;
  }
  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);
  if (left && right) {
    return root;
  }
  return left || right;
};
```

# 235. 二叉搜索树的最近公共祖先

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */

/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function (root, p, q) {
  const val = root.val;
  if (p.val < val && q.val < val) {
    return lowestCommonAncestor(root.left, p, q);
  }
  if (p.val > val && q.val > val) {
    return lowestCommonAncestor(root.right, p, q);
  }
  return root;
};
```

# 701. 二叉搜索树中的插入操作

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */
var insertIntoBST = function (root, val) {
  if (root == null) {
    return new TreeNode(val);
  }
  let cur = root;
  while (cur !== null) {
    if (cur.val > val) {
      if (cur.left) {
        cur = cur.left;
      } else {
        cur.left = new TreeNode(val);
        break;
      }
    } else {
      if (cur.right) {
        cur = cur.right;
      } else {
        cur.right = new TreeNode(val);
        break;
      }
    }
  }
  return root;
};
```

# 450. 删除二叉搜索树中的节点

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} key
 * @return {TreeNode}
 */
var deleteNode = function (root, key) {
  if (root === null) {
    return null;
  }
  if (root.val < key) {
    root.right = deleteNode(root.right, key);
  }
  if (root.val > key) {
    root.left = deleteNode(root.left, key);
  }
  if (root.val === key) {
    if (!root.left && !root.right) {
      return null;
    }
    if (!root.left) {
      return root.right;
    }
    if (!root.right) {
      return root.left;
    }
    let cur = root.right;
    while (cur.left) {
      cur = cur.left;
    }
    cur.left = root.left;
    return root.right;
  }
  return root;
};
```

# 669. 修剪二叉搜索树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} low
 * @param {number} high
 * @return {TreeNode}
 */
var trimBST = function (root, low, high) {
  if (root === null) {
    return null;
  }
  if (root.val < low) {
    return trimBST(root.right, low, high);
  } else if (root.val > high) {
    return trimBST(root.left, low, high);
  } else {
    root.left = trimBST(root.left, low, high);
    root.right = trimBST(root.right, low, high);
    return root;
  }
};
```

# 108. 将有序数组转换为二叉搜索树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function (nums) {
  const dfs = (left, right) => {
    if (left === right) {
      return null;
    }
    const k = Math.floor((left + right) / 2);
    return new TreeNode(nums[k], dfs(left, k), dfs(k + 1, right));
  };
  return dfs(0, nums.length);
};
```

# 538. 把二叉搜索树转换为累加树

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var convertBST = function (root) {
  let sum = 0;
  const dfs = (node) => {
    if (node === null) {
      return;
    }
    dfs(node.right);
    sum += node.val;
    node.val = sum;
    dfs(node.left);
  };
  dfs(root);
  return root;
};
```