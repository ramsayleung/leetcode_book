+++
title = "328. Odd Even Linked List"
author = ["Ramsay Leung"]
date = 2022-03-24T22:01:00+08:00
lastmod = 2022-03-24T22:08:04+08:00
draft = false
weight = 328
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/odd-even-linked-list/>
Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return the reordered list.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1**:
![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

```text
Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]
```

**Example 2**:
![](https://assets.leetcode.com/uploads/2021/03/10/oddeven2-linked-list.jpg)

```text
Input: head = [2,1,3,5,6,4,7]
Output: [2,3,6,7,1,5,4]
```

**Constraints**:

-   `n ==` number of nodes in the linked list
-   `0 <= n <= 10^4`
-   `-10^6 <= Node.val <= 10^6`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/328-odd-even-linked-list.png" link="/ox-hugo/328-odd-even-linked-list.png" >}}

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
  ListNode* oddEvenList(ListNode* head) {
    // Time complexity: O(N) N is the size of linked list
    // Space complexity: O(1)
    if(!head){
      return head;
    }

    ListNode* first_even = nullptr;
    ListNode* first_odd = nullptr;
    ListNode* last_even = nullptr;
    ListNode* last_odd = nullptr;
    int index = 1;

    while(head){
      if(index % 2 == 1){
	first_odd = (first_odd ==nullptr? head: first_odd);

	if(!last_odd){
	  last_odd = head;
	}else{
	  last_odd -> next = head;
	  last_odd = last_odd->next;
	}
      } else{
	first_even = (first_even == nullptr? head: first_even);

	if(!last_even){
	  last_even = head;
	}else{
	  last_even -> next = head;
	  last_even = last_even->next;
	}
      }

      head = head-> next;
      index ++;
    }

    if(last_even){
      last_even -> next = nullptr;
    }

    if(last_odd){
      last_odd -> next = first_even;
    }

    return first_odd;
  }
};
```
