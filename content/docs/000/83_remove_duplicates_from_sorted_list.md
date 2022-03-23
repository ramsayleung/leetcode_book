+++
title = "83. Remove Duplicates from Sorted List"
author = ["Ramsay Leung"]
date = 2022-03-22T23:19:00+08:00
lastmod = 2022-03-23T21:05:13+08:00
draft = false
weight = 83
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/remove-duplicates-from-sorted-list/>

Given the `head` of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list **sorted** as well.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/01/04/list1.jpg" >}}

```text
Input: head = [1,1,2]
Output: [1,2]
```

**Example 2**:
![](https://assets.leetcode.com/uploads/2021/01/04/list2.jpg)

```text
Input: head = [1,1,2,3,3]
Output: [1,2,3]
```

**Constraints**:

-   The number of nodes in the list is in the range `[0, 300]`.
-   `-100 <= Node.val <= 100`
-   The list is guaranteed to be **sorted** in ascending order.


## <span class="section-num">2</span> Solution {#solution}

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
  ListNode* deleteDuplicates(ListNode* head) {
    // time complexity: O(N): N is size of linked list
    // space compleixty: O(1)
    if(!head){
      return head;
    }

    ListNode* prev = nullptr;
    ListNode* result = head;
    while(head){
      if(!prev){
	prev = head;
	continue;
      }

      if(prev->val != head->val){
	prev->next = head;
	prev = prev->next;
      }else{
	// delete the last duplicate node
	if(!head->next){
	  prev -> next = nullptr;
	  return result;
	}
      }

      head = head -> next;
    }

    return result;
  }
};
```
