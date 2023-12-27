+++
title = "Valid Parantheses --- Solution and Analysis"
date = "2023-10-24T14:10:55-07:00"
author = "Andrew Attilio"
authorTwitter = "" #do not include @
cover = ""
tags = ["dsa", "arrays"]
keywords = ["", ""]
description = "Solution and analysis for the Valid Parantheses Leetcode problem."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## The Challenge

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

- Open brackets must be closed by the same type of brackets.
- Open brackets must be closed in the correct order.
- Every close bracket has a corresponding open bracket of the same type.

## Solution

```
class Solution(object):
    def isValid(self, s):
        stack = []
        pairs = {
            '(': ')',
            '{': '}',
            '[': ']'
        }

        for bracket in s:
            if bracket in pairs:
                stack.append(bracket)
            elif len(stack) == 0 or bracket != pairs[stack.pop()]:
                return False

        return len(stack) == 0
```

This is a clear-cut problem where a stack is an intuitive solution. We initialize an empty stack and iterate through the list of brackets. If it is a left bracket, denoted by it being a key in the dictionary, then we append to the stack.

If it is not a left, then it must be a right bracket. Therefore, we check if the stack is empty (which makes this an invalid bracket) or if the bracket in question pairs does *not* pair with the most recent bracket on the stack (which we pop off simultaneously).

If we get to the end and the stack is empty, the return statement will be True. Otherwise, it will be False.
```