+++
title = "141. Linked list cycle"
date = 2020-04-28T09:04:58
lastmod = 2022-03-27T10:16:14+08:00
tags = ["linked_list"]
categories = ["linked_list"]
draft = false
weight = 141
toc = true
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/linked-list-cycle/>

Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

**Example 1**:

```text
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

{{< figure src="/ox-hugo/2020-04-28_09-55-10_circularlinkedlist.png" >}}

**Example 2**:

```text
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

{{< figure src="/ox-hugo/2020-04-28_09-55-28_circularlinkedlist_test2.png" >}}

**Example 3**:

```text
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.
```

{{< figure src="/ox-hugo/2020-04-28_09-55-41_circularlinkedlist_test3.png" >}}

**Follow up**:

Can you solve it using O(1) (i.e. constant) memory?


## <span class="section-num">2</span> Solution {#solution}

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
# time complexity: O(n), n is the length of linkedList
# space complexity: O(n), n is the size of seen set.
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
	seen = set()
	while head:
	    if head in seen:
		return True
	    seen.add(head)
	    head = head.next
	return False
```

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
  bool hasCycle(ListNode *head) {
    // Runtime complexity: O(n); n is the size of linked_list
    // Space complexity: O(1)
    if(!head){
      return false;
    }

    ListNode* fast = head -> next;
    while(head){
      // if the fast pointer meets the slow pointer, there is a cycle
      if (fast == head){
	return true;
      }

      if(fast && fast ->next){
	fast = fast->next->next;
      } else{
	// if there is a cycle, the fast-> next will never be null
	return false;
      }

      head = head->next;
    }

    return false;
  }
};
```
