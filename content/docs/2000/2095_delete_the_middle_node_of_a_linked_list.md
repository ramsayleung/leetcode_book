+++
title = "2095. Delete the Middle Node of a Linked List"
author = ["Ramsay Leung"]
date = 2022-03-27T10:37:00+08:00
lastmod = 2022-03-27T10:44:09+08:00
draft = false
weight = 2095
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/>

You are given the `head` of a linked list. **Delete** the **middle node**, and return the `head` of the modified linked list.

The **middle node** of a linked list of size `n` is the `⌊n / 2⌋th` node from the **start** using **0-based indexing**, where `⌊x⌋` denotes the largest integer less than or equal to `x`.

For `n` = `1, 2, 3, 4`, and `5`, the middle nodes are `0, 1, 1, 2`, and `2`, respectively.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/11/16/eg1drawio.png" >}}

```text
Input: head = [1,3,4,7,1,2,6]
Output: [1,3,4,1,2,6]
Explanation:
The above figure represents the given linked list. The indices of the nodes are written below.
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.
We return the new list after removing this node.
```

**Example 2**:

{{< figure src="https://assets.leetcode.com/uploads/2021/11/16/eg2drawio.png" >}}

```text
Input: head = [1,2,3,4]
Output: [1,2,4]
Explanation:
The above figure represents the given linked list.
For n = 4, node 2 with value 3 is the middle node, which is marked in red.
```

**Example 3**:

{{< figure src="https://assets.leetcode.com/uploads/2021/11/16/eg3drawio.png" >}}

```text
Input: head = [2,1]
Output: [2]
Explanation:
The above figure represents the given linked list.
For n = 2, node 1 with value 1 is the middle node, which is marked in red.
Node 0 with value 2 is the only node remaining after removing node 1.
```

**Constraints**:

-   The number of nodes in the list is in the range `[1, 10^5]`.
-   `1 <= Node.val <= 10^5`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/2095-delete-the-middle-node-of-a-linked-list.png" link="/ox-hugo/2095-delete-the-middle-node-of-a-linked-list.png" >}}

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* deleteMiddle(ListNode* head) {
	// Time complexity: O(1.5N) = O(N). N is the size of linked list
	// Space complexity: O(1)
	if(!head){
	    return head;
	}

	int size = 0;
	ListNode* first = head;
	while(first){
	    size++;
	    first = first->next;
	}

	if(1 == size){
	    return nullptr;
	}

	int middle = size / 2;
	int index = 0;
	first = head;
	while(first){
	    if(index == middle - 1){
		// the prev node of middle node
		first->next = first->next->next;
		break;
	    }

	    index ++;
	    first = first->next;
	}

	return head;
    }
};
```
