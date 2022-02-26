+++
title = "61. Rotate List"
date = 2022-02-15T22:12:26
lastmod = 2022-02-26T20:11:20+08:00
tags = ["linked_list"]
categories = ["linked_list"]
draft = false
toc = true
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/rotate-list/>

Given the head of a linked list, rotate the list to the right by k places.

Example 1:

{{< figure src="https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg" >}}

```text
Input: head = [1,2,3,4,5], k = 2
Output: [4,5,1,2,3]
```

Example 2:

{{< figure src="https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg" >}}

```text
Input: head = [0,1,2], k = 4
Output: [2,0,1]
```

**Constraints**:

-   The number of nodes in the list is in the range `[0, 500]`.
-   `-100 <= Node.val <= 100`
-   `0 <= k <= 2 * 10^9`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/61_rotate_list.png" link="/ox-hugo/61_rotate_list.png" >}}

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
  ListNode* rotateRight(ListNode* head, int k) {
    // time complexity: O(n)
    // space complexity: O(1)

    if (k == 0 || !head){
      return head;
    }

    int size = 0;
    ListNode* first = head;
    ListNode* last_node = head;
    while(first){
      if(first && nullptr == first->next){
	last_node = first;
      }
      first = first -> next;

      size ++;
    }

    // it will be the same linked_list after rotate `size` steps
    k = k % size;
    if(k ==0){
      return head;
    }

    // split the linked list into two single linked lists by the rotate point;
    ListNode* k_minus_1 = head;
    for(int i = 0; i < size - k - 1; i++){
      k_minus_1 = k_minus_1 ->next;
    }

    ListNode* k_node = k_minus_1 -> next; // the rotate point
    k_minus_1 -> next = nullptr;
    last_node -> next = head;

    return k_node;
  }
};
```
