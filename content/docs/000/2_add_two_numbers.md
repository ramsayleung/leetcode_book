+++
title = "2. Add two number"
author = ["Ramsay Leung"]
date = 2020-04-24T21:45:43
lastmod = 2022-02-27T20:07:12+08:00
draft = false
weight = 2
+++

## <span class="section-num">1</span> Description {#description}

source: <https://leetcode.com/problems/add-two-numbers/>

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

{{< figure src="https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg" >}}

```text
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```


## <span class="section-num">2</span> Solution {#solution}

Solution in Python3:

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Runtime: 72 ms, faster than 62.00% of Python3 online submissions for Add Two Numbers.
# time complexity: O(n1+n2), n1 is the length of l1, n2 is the length of l2
# space complexity: O(max(n1,n2)), the length of sum of two number equals the larger's


class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
	num1 = self.getNumber(l1)
	num2 = self.getNumber(l2)
	result = num1+num2
	return self.constructNumber(result)

    def getNumber(self, llist: ListNode) -> int:
	num = ""
	while llist:
	    num = str(llist.val) + num
	    llist = llist.next
	return int(num)

    def constructNumber(self, num: int) -> ListNode:
	print(num)
	input = str(num)
	parent = root = None
	while len(input) > 0:
	    val = input[len(input)-1]
	    newNode = ListNode(int(val))
	    if not parent:
		parent = newNode
		root = parent
	    else:
		parent.next = newNode
		parent = newNode
	    input = input[:len(input)-1]
	return root

```

Solution in C++:

{{< figure src="/ox-hugo/2_add_two_numbers.png" link="/ox-hugo/2_add_two_numbers.png" >}}

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
  ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
    // Runtime complexity O(n), n = max(l1.size(), l2.size())
    // Space complexity O(1)

    ListNode *result = l1;
    ListNode *prev = nullptr;
    int carry = 0;
    while (l1 && l2) {
      int add_result = l1->val + l2->val + carry;
      if (add_result % 10 == add_result) {
	l1->val = add_result;
	carry = 0;
      } else {
	l1->val = add_result % 10;
	carry = 1;
      }

      prev = l1;
      l1 = l1->next;
      l2 = l2->next;
    }

    if (l1 || l2) {
      prev->next = (l1 != nullptr ? l1 : l2);
      ListNode *head = prev->next;

      while (head) {
	int add_result = head->val + carry;
	if (add_result % 10 == add_result) {
	  head->val = add_result;
	  carry = 0;
	} else {
	  head->val = add_result % 10;
	  carry = 1;
	}
	prev = head;
	head = head->next;
      }
    } else {
      if (carry != 0) {
	prev->next = new ListNode(carry);
	return result;
      }
    }

    if (carry != 0) {
      prev->next = new ListNode(carry);
    }

    return result;
  }
};
```
