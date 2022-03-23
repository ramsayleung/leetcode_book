+++
title = "24. Swap Nodes in Pairs"
author = ["Ramsay Leung"]
date = 2022-03-22T09:03:00+08:00
lastmod = 2022-03-22T09:33:55+08:00
draft = false
weight = 24
+++

## <span class="section-num">1</span> Description {#description}

Given a linked list, swap every two adjacent nodes and return its head. You must solve the problem without modifying the values in the list's nodes (i.e., only nodes themselves may be changed.)

Example 1:

{{< figure src="https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg" >}}

```text
Input: head = [1,2,3,4]
Output: [2,1,4,3]
```

Example 2:

```text
Input: head = []
Output: []
```

Example 3:

```text
Input: head = [1]
Output: [1]
```

**Constraints**:

-   The number of nodes in the list is in the range `[0, 100]`.
-   `0 <= Node.val <= 100`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/24_swap_nodes_in_pair.png" link="/ox-hugo/24_swap_nodes_in_pair.png" >}}

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
  ListNode* swapPairs(ListNode* head) {
    // Time complexity: O(N) N = S / 2, S is the length of linked-list
    // Space Complexity: O(1)
    if(!head || !head->next){
      return head;
    }

    ListNode* result = head->next;
    ListNode* prev = nullptr;
    while(head){
      auto right = head->next;
      if(right){
	head->next = right->next;
	right->next = head;
	if (prev){
	  prev->next = right;
	}
      }

      prev = head;
      head= head->next;
    }

    return result;
  }
};
```
