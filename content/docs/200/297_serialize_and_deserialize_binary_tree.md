+++
title = "297. Serialize and Deserialize Binary Tree"
author = ["Ramsay Leung"]
date = 2022-05-27T20:59:00+08:00
lastmod = 2022-05-27T21:02:54+08:00
draft = false
weight = 297
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/serialize-and-deserialize-binary-tree/>

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Clarification**: The input/output format is the same as how [LeetCode serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" link="https://assets.leetcode.com/uploads/2020/09/15/serdeser.jpg" >}}

```text
Input: root = [1,2,3,null,null,4,5]
Output: [1,2,3,null,null,4,5]
```

**Example 2**:

```text
Input: root = []
Output: []
```

**Constraints**:

-   The number of nodes in the tree is in the range `[0, 10^4]`.
-   `-1000 <= Node.val <= 1000`


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
// Codec ser, deser;
// TreeNode* ans = deser.deserialize(ser.serialize(root));
```
