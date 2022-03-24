+++
title = "86. Partition List"
author = ["Ramsay Leung"]
date = 2022-03-24T21:05:00+08:00
lastmod = 2022-03-24T21:28:33+08:00
draft = false
weight = 86
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/partition-list/>

Given the `head` of a linked list and a value `x`, partition it such that all nodes **less than** `x` come before nodes **greater than or equal** to `x`.

You should **preserve** the original relative order of the nodes in each of the two partitions.

**Example 1**:

{{< figure src="https://assets.leetcode.com/uploads/2021/01/04/partition.jpg" >}}

```text
Input: head = [1,4,3,2,5,2], x = 3
Output: [1,2,2,4,3,5]
```

**Example 2**:

```text
Input: head = [2,1], x = 2
Output: [1,2]
```

**Constraints**:

-   The number of nodes in the list is in the range `[0, 200]`.
-   `-100 <= Node.val <= 100`
-   `-200 <= x <= 200`


## <span class="section-num">2</span> Solution {#solution}

{{< figure src="/ox-hugo/86_partition_list.png" link="/ox-hugo/86_partition_list.png" >}}

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
  ListNode *partition(ListNode *head, int x) {
    // Time complexity: O(N), N is the size of linked_list
    // Space complexity: O(1)
    if (!head) {
      return head;
    }

    ListNode *first_less_x = nullptr;
    ListNode *last_less_x = nullptr;
    ListNode *last_greater_x = nullptr;
    ListNode *first_greater_x = nullptr;
    while (head) {
      if (head->val < x) {
	first_less_x = (first_less_x == nullptr ? head : first_less_x);

	if (!last_less_x) {
	  last_less_x = head;

	} else {
	  last_less_x->next = head;
	  last_less_x = last_less_x->next;
	}
      } else {
	first_greater_x = (first_greater_x == nullptr ? head : first_greater_x);

	if (!last_greater_x) {
	  last_greater_x = head;
	} else {
	  last_greater_x->next = head;
	  last_greater_x = last_greater_x->next;
	}
      }

      head = head->next;
    }

    if (last_greater_x) {
      last_greater_x->next = nullptr;
    }

    if (last_less_x) {
      last_less_x->next = first_greater_x;
    }

    return first_less_x != nullptr ? first_less_x : first_greater_x;
  }
};
```
