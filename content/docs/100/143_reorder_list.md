+++
title = "143. Reorder List"
author = ["Ramsay Leung"]
date = 2022-03-27T09:55:00+08:00
lastmod = 2022-03-27T10:15:21+08:00
draft = false
weight = 143
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/reorder-list/>
You are given the head of a singly linked-list. The list can be represented as:

```text
L0 → L1 → … → Ln - 1 → Ln
```

Reorder the list to be on the following form:

```text
L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
```

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/03/04/reorder1linked-list.jpg" >}}

```text
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

**Example 2**:

{{< figure src="https://assets.leetcode.com/uploads/2021/03/09/reorder2-linked-list.jpg" >}}

```text
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

**Constraints**:

-   The number of nodes in the list is in the range `[1, 5 * 10^4]`.
-   `1 <= Node.val <= 1000`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/143-reorder-list.png" link="/ox-hugo/143-reorder-list.png" >}}

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
#include <deque>
class Solution {
public:
  void reorderList(ListNode* head) {
    // Time complexity: O(2N), N is the size of linked list
    // Space complexity: O(N), N is the size of linked list
    std::deque<ListNode*> head_deque;
    while(head){
      head_deque.push_back(head);
      head = head->next;
    }

    ListNode* prev = nullptr;
    ListNode* node = nullptr;
    bool first_last_flag = true;

    while(!head_deque.empty()){
      if(first_last_flag){
	node = head_deque.front();
	head_deque.pop_front();
      }else{
	node = head_deque.back();
	head_deque.pop_back();
      }

      node -> next = nullptr;
      first_last_flag = !first_last_flag;

      if(prev){
	prev->next = node;
	prev = prev->next;
      }else{
	prev = node;
      }

      if(!head){
	head = node;
      }
    }
  }
};
```
