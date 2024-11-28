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