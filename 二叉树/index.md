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