+++
title = "230. Kth Smallest Element in a BST"
author = ["Ramsay Leung"]
date = 2022-04-29T23:34:00+08:00
lastmod = 2022-05-08T08:18:46+08:00
draft = false
weight = 230
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/kth-smallest-element-in-a-bst/>

Given the `root` of a binary search tree, and an integer `k`, return the `k^th` smallest value (**1-indexed**) of all the values of the nodes in the tree.

Example 1:

{{< figure src="https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg" link="https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg" >}}

```text
Input: root = [3,1,4,null,2], k = 1
Output: 1
```

Example 2:

{{< figure src="https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg" link="https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg" >}}

```text
Input: root = [5,3,6,2,4,null,null,1], k = 3
Output: 3
```

**Constraints**:

The number of nodes in the tree is n.

-   `1 <= k <= n <= 10^4`
-   `0 <= Node.val <= 10^4`

Follow up: If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?


## <span class="section-num">2</span> Solution {#solution}

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
	// Time complexity: O(N)
	// Space compleixty: O(1)
	preorder(root,k );
	return kth_value;
    }

    void preorder(TreeNode* root, int k){
	if(!root){
	    if(-1 == kth){
		kth = 0;
	    }
	    return;
	}else{
	    preorder(root->left, k);
	    kth ++;
	    if (kth == k){
		kth_value = root->val;
	    }
	    preorder(root->right,k );
	    return;

	}
    }
int kth_value = -1;
int kth = -1;
};
```
