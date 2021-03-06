# 82. Remove Duplicates from Sorted List II

## Problem
- Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

> For example,
> 
> Given 1->2->3->3->4->4->5, return 1->2->5.
> 
> Given 1->1->1->2->3, return 2->3.

## Solution
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        dummy.next = head
        pre, cur = dummy, head
        tmp = None
        while cur:
            if tmp != cur.val and (cur.next is None or cur.val != cur.next.val):
                pre.next = cur
                pre = cur
            tmp = cur.val
            cur = cur.next
            pre.next = None
        return dummy.next
```
