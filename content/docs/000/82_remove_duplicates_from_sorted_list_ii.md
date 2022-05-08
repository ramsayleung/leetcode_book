+++
title = "82. Remove Duplicates from Sorted List II"
author = ["Ramsay Leung"]
date = 2022-04-30T08:59:00+08:00
lastmod = 2022-05-08T08:15:30+08:00
draft = false
weight = 82
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/>

Given the `head` of a **sorted** linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg" link="https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg" >}}

```text
Input: head = [1,2,3,3,4,4,5]
Output: [1,2,5]
```

**Example 2**:

{{< figure src="https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg" link="https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg" >}}

```text
Input: head = [1,1,1,2,3]
Output: [2,3]
```

**Constraints**:

-   The number of nodes in the list is in the range `[0, 300]`.
-   `-100 <= Node.val <= 100`
-   The list is guaranteed to be **sorted** in ascending order.


## <span class="section-num">2</span> Solution {#solution}

```C++
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
  ListNode* deleteDuplicates(ListNode* head) {
    // Space complexity: O(1)
    // Time complexity: O(N)
    ListNode fake_head(0, head);
    ListNode *prev = &fake_head;
    while(head){
      if(head->next && head->next->val == head->val){
	// loop until the last node of the sublist needed to delete
	// e.g. [3, 3]
	while(head->next && head->next->val == head->val){
	  head = head->next;
	}

	// let the `prev` node point to the next node of the last node of the subset
	// it doesn't matter if the head->next is duplicated either, since we could loop head->next again until we find the last node of `head-next`.
	prev->next = head->next;
      } else{
	prev = prev->next;
      }

      head = head->next;
    }

    return fake_head.next;
  }
};
```
