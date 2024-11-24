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