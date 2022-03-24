+++
title = "203. Remove Linked List Elements"
author = ["Ramsay Leung"]
date = 2022-03-24T21:24:00+08:00
lastmod = 2022-03-24T21:28:25+08:00
draft = false
weight = 203
+++

## <span class="section-num">1</span> Description {#description}

Given the `head` of a linked list and an integer `val`, remove all the nodes of the linked list that has `Node.val == val`, and return the new head.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg" >}}

```text
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]
```

**Example 2**:

```text
Input: head = [], val = 1
Output: []
```

**Example 3**:

```text
Input: head = [7,7,7,7], val = 7
Output: []
```

**Constraints**:

-   The number of nodes in the list is in the range `[0, 10^4]`.
-   `1 <= Node.val <= 50`
-   `0 <= val <= 50`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/203-remove-linked-list-elements.png" link="/ox-hugo/203-remove-linked-list-elements.png" >}}

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
  ListNode* removeElements(ListNode* head, int val) {
    // Time complexity: O(N), N is the size of linked list
    // Space complexity: O(1)
    if(!head){
      return head;
    }

    ListNode* prev = nullptr;
    ListNode* result = nullptr;
    while(head){
      if(head->val == val){
	if(prev){
	  prev->next = head->next;
	  head = head->next;
	}else{
	  ListNode* next = head->next;
	  head->next = nullptr;
	  head = next;
	}
      }else{
	prev = head;
	head = head->next;
      }

      result = (result ==nullptr? prev: result);
    }

    return result;
  }
};
```
