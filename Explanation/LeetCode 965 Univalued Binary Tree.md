# LeetCode 965: Univalued Binary Tree

A binary tree is *univalued* if every node in the tree has the same value.

Return `true` if and only if the given tree is univalued.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/28/unival_bst_1.png)

```
nput: [1,1,1,1,1,null,1]
Output: true
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/28/unival_bst_2.png)

```
Input: [2,2,2,5,2]
Output: false 
```

**Note:**

1. The number of nodes in the given tree will be in the range `[1, 100]`.
2. Each node's value will be an integer in the range `[0, 99]`.

## Java

```java
package com.blessed.leetcode.easy;


public class LeetCode965 {
    boolean flag = true;
    public boolean isUnivalTree(TreeNode root) {
        if (root.left != null) {
            if (root.val != root.left.val) {
                flag = false;
            }
            isUnivalTree(root.left);
        }
        if (root.right != null) {
            if (root.val != root.right.val) {
                flag = false;
            }
            isUnivalTree(root.right);
        }
        return flag;
    }

    public static void main(String[] args) {
        TreeNode t1 = new TreeNode(9);
        TreeNode t2 = new TreeNode(9);
        TreeNode t3 = new TreeNode(6);
        TreeNode t4 = new TreeNode(9);
        TreeNode t5 = new TreeNode(9);
        t1.left = t2;
        t1.right = t3;
        t2.left = t4;
        t2.right = t5;

        LeetCode965 solution = new LeetCode965();
        System.out.println(solution.isUnivalTree(t1));
    }
}

class TreeNode {

    int val;
    TreeNode left;
    TreeNode right;

    public TreeNode(int value) {
        this.val = value;
    }
}

```

## Python

```python
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


class Solution:
    def isUnivalTree(self, root):
        """

        :param root: TreeNode
        :return: bool
        """
        def traverse(node, parent):
            if node is None:
                return True
            if node.val is not parent.val:
                return False
            return traverse(node.left, node) and traverse(node.right, node)
        return traverse(root, root)


if __name__ == '__main__':
    t1 = TreeNode(9)
    t2 = TreeNode(9)
    t3 = TreeNode(6)
    t4 = TreeNode(9)
    t5 = TreeNode(9)
    t1.left = t2
    t1.right = t3
    t2.left = t4
    t2.right = t5

    solution = Solution()
    isUnivalTree = solution.isUnivalTree(t1)
    print(isUnivalTree)

```

## 分析

这是一道简单的二叉树遍历的问题。问题的边界条件需要注意，什么时候代表着遍历完成需要考虑。

二叉树遍历：

- 先序遍历
  - 访问根节点
  - 先序遍历左子树
  - 先序遍历右子树
- 中序遍历
  - 中序遍历左子树
  - 访问根节点
  - 中序遍历右子树
- 后序遍历
  - 后序遍历左子树
  - 后序遍历右子树
  - 访问根节点

