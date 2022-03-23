+++
title = "1721. Swapping Nodes in a Linked List"
author = ["Ramsay Leung"]
date = 2022-03-22T21:49:00+08:00
lastmod = 2022-03-23T21:06:00+08:00
draft = false
weight = 1721
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/swapping-nodes-in-a-linked-list/>
You are given the `head` of a linked list, and an integer `k`.

Return the head of the linked list after **swapping** the values of the `kth` node from the beginning and the `kth` node from the end (the list is **1-indexed**).

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2020/09/21/linked1.jpg" >}}

```text
Input: head = [1,2,3,4,5], k = 2
Output: [1,4,3,2,5]
```

**Example 2**:

```text
Input: head = [7,9,6,6,7,8,3,0,9,5], k = 5
Output: [7,9,6,6,8,7,3,0,9,5]
```

**Constraints**:

-   The number of nodes in the list is `n`.
-   `1 <= k <= n <= 10^5`
-   `0 <= Node.val <= 100`


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
  ListNode* swapNodes(ListNode* head, int k) {
    // time complexity: O(2N) = O(N), N = size of linked list
    // space compleixty(1)
    int size = 0;
    ListNode* first = head;
    ListNode* kth_from_begin = nullptr;
    ListNode* kth_from_end = nullptr;
    while(first){
      size++;
      if(size == k){
	kth_from_begin = first;
      }

      first = first->next;
    }


    int next_round_size = 0;
    first = head;
    while(first){
      next_round_size++;


      if(next_round_size == size - k + 1){
	kth_from_end = first;
	break;
      }
      first = first->next;
    }

    int tmp = kth_from_begin -> val;
    kth_from_begin->val = kth_from_end->val;
    kth_from_end -> val = tmp;

    return head;
  }
};
```
