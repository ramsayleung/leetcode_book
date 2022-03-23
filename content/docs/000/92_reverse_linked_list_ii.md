+++
title = "92. Reverse Linked List II"
author = ["Ramsay Leung"]
date = 2022-03-23T12:52:00+08:00
lastmod = 2022-03-23T21:04:42+08:00
draft = false
weight = 92
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/reverse-linked-list-ii/>

Given the `head` of a singly linked list and two integers `left` and `right` where `left <` right=, reverse the nodes of the list from position `left` to position `right`, and return the reversed list.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/02/19/rev2ex2.jpg" >}}

```text
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]
```

**Example 2**:

```text
Input: head = [5], left = 1, right = 1
Output: [5]
```

**Constraints**:

The number of nodes in the list is `n`.

-   `1 <= n <= 500`
-   `-500 <= Node.val <= 500`
-   `1 <= left <= right <= n`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/92_reverse_linked_list_ii.png" link="/ox-hugo/92_reverse_linked_list_ii.png" >}}

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
  ListNode* reverseBetween(ListNode* head, int left, int right) {
    // time complexity: O(2N), N = size of the linked list
    // space compleixty: O(1)
    if(!head || left == right){
      return head;
    }

    ListNode* left_prev = nullptr;
    ListNode* left_node = nullptr;
    ListNode* right_node = nullptr;
    ListNode* result = nullptr;

    int size = 0;
    while(head){
      size ++;
      if(!result && size <= left - 1){
	result = head;
      }
      if(size == left - 1){
	left_prev = head;
      }

      if(size == left){
	left_node = head;
      }


      if(size == right){
	right_node = head;
      }

      head = head->next;
    }

    ListNode* right_node_next = right_node -> next;
    right_node-> next = nullptr;
    if(!result){
      result = right_node;
    }

    while(left_node){
      ListNode* left_next = left_node->next;
      left_node->next = right_node_next;
      right_node_next = left_node;
      if(!left_next && left_prev){
	left_prev -> next = left_node;
      }
      left_node = left_next;
    }



    return result;
  }
};
```
