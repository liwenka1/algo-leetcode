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