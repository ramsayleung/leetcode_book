+++
title = "449. Serialize and Deserialize BST"
author = ["Ramsay Leung"]
date = 2022-05-27T20:56:00+08:00
lastmod = 2022-05-27T20:59:43+08:00
draft = false
weight = 449
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/serialize-and-deserialize-bst/>

Serialization is converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a **binary search tree**. There is no restriction on how your serialization/deserialization algorithm should work. You need to ensure that a binary search tree can be serialized to a string, and this string can be deserialized to the original tree structure.

**The encoded string should be as compact as possible.**

**Example 1**:

```text
Input: root = [2,1,3]
Output: [2,1,3]
```

**Example 2**:

```text
Input: root = []
Output: []
```

**Constraints**:

-   The number of nodes in the tree is in the range `[0, 10^4]`.
-   `0 <= Node.val <= 10^4`
-   The input tree is **guaranteed** to be a binary search tree.


## <span class="section-num">2</span> Solution {#solution}

```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
#include <cstdlib>
#include <sstream>
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
	// time complexity: O(N), N is the node number of tree.
	// space complexity: O(N)
	std::stringstream ss;
	dfs_serialize(root, ss);
	return ss.str();

    }

    void dfs_serialize(TreeNode* root, std::stringstream& ss){
	// pre-order
	if(root){
	    ss << std::to_string(root->val) << "|";
	    dfs_serialize(root->left, ss);
	    dfs_serialize(root->right, ss);
	}else{
	    // represent null as *
	    ss << "*|";
	}
    }


    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
	// time complexity: O(N)
	// space complexity: O(N)
	int index = 0;
	return dfs_deserialize(data, index);
    }


    TreeNode* dfs_deserialize(const string& data, int& index) {
	if(index >= data.size()){
	    return nullptr;
	}

	int start = index;
	while(data[index] != '|'){
	    index++;
	}

	std::string token = data.substr(start, index - start);

	if(token == "*"){
	    return nullptr;
	}

	TreeNode *node = new TreeNode(std::atoi(token.c_str()));
	// data[index] = "|"
	index++;
	node->left = dfs_deserialize(data, index);

	index++;
	node->right = dfs_deserialize(data, index);

	return node;

    }
};

// Your Codec object will be instantiated and called as such:
// Codec* ser = new Codec();
// Codec* deser = new Codec();
// string tree = ser->serialize(root);
// TreeNode* ans = deser->deserialize(tree);
// return ans;
```
