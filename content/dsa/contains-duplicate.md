+++
title = "Contains Duplicate --- Solution and Analysis"
date = "2023-11-09T14:10:55-07:00"
author = "Andrew Attilio"
authorTwitter = "" #do not include @
cover = ""
tags = ["dsa", "arrays"]
keywords = ["", ""]
description = "Solution and analysis for the Contains Duplicate Leetcode problem."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## The Challenge

Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

```
Example 1:

Input: nums = [1,2,3,1]
Output: true

Example 2:

Input: nums = [1,2,3,4]
Output: false

Example 3:

Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

### Solution

This is a rather simple problem to solve in O(n) time. First, we create a set that tracks the numbers we have seen. For each number in the list, we check it against the list. If its in the list, we found a duplicate. If not, we add it to the seen set and continue iterating. 

If we make it all the way through, we return False.

```
class Solution(object):
def containsDuplicate(self, nums):
    has_appeared = set()
    for i in nums:
        if i in has_appeared:
            return True
        has_appeared.add(i)
    return False
```