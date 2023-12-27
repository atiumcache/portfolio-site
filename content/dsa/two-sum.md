+++
title = "Two Sum --- Solution and Analysis"
date = "2023-11-09T14:10:55-07:00"
author = "Andrew Attilio"
authorTwitter = "" #do not include @
cover = ""
tags = ["dsa", "arrays"]
keywords = ["", ""]
description = "Solution and analysis for the Two Sum Leetcode problem."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## The Challenge

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

## Solution

The naive approach is nested for loops, where we iterate through each element `i` and compare it to each element `j`. This has a time complexity of O(n^2) due to iterating through nums n*n times.

An objectively better approach is to utilize a hash map. We can iterate through the list only once, checking if the current number has a complementary number in the hash_table that adds to the target. If they do, we return a list with the two indices. If not, we add `nums[i]` to the hash table and continue iterating. This approach has a time complexity of O(n) because we iterate through the list only once.

```
class Solution(object):
def twoSum(self, nums, target):
    hash_table = {}

    for i in range(len(nums)):
        if target - nums[i] in hash_table:
            return [hash_table[target-nums[i]], i]
        hash_table[nums[i]] = i

    return [] # no matches
```