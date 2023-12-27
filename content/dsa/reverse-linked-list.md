+++
title = "Reverse Linked List --- Solution and Analysis"
date = "2023-11-09T14:10:55-07:00"
author = "Andrew Attilio"
authorTwitter = "" #do not include @
cover = ""
tags = ["dsa", "arrays"]
keywords = ["", ""]
description = "Solution and analysis for the Reverse Linked List Leetcode problem."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## The Challenge

Given the head of a singly linked list, reverse the list, and return the reversed list.

```
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Some built-in Node functions are defined in the comments. When the head is passed in, it is pointing to the next node in the list, and so on. The end of the list is reached when a node's next value is None/NULL. Therefore, we set the prev node to NULL initially, so that when we reverse-engineer, the head will be the new end of the list.

## Solution

We keep track of the current node, starting with the head. While the current head != None (in other words, while we haven't passed the end of the list), we make next a temporary pointer to the current's next. Then, with current.next freed up by the temp pointer, we point current.next to the prev node. In the case of head, it is now pointing to NULL. Then, we change prev to the current node (so, in case 1, the head is now the previous node). Finally, we move our current node to the next in the list.

Once current passes the last node and reaches NULL, we return that last node (which is now pointed to by prev). This returns a reversed list, where the originally-last node is now the head, and each 'next' is pointing 'backwards' in regards to the original list.

```
class Solution(object):
    def reverseList(self, head):
        prev = None
        current = head
        while current != None:
            next = current.next
            current.next = prev
            prev = current
            current = next
        return prev
```