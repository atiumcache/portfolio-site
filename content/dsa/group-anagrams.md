+++
title = "Group Anagrams --- Solution and Analysis"
date = "2023-11-11T14:10:55-07:00"
author = "Andrew Attilio"
authorTwitter = "" #do not include @
cover = ""
tags = ["dsa", "arrays"]
keywords = ["", ""]
description = "Solution and analysis for the Group Anagrams Leetcode problem."
showFullContent = false
readingTime = false
hideComments = false
color = "" #color from the theme settings
+++

## The Challenge

Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

```
Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:
Input: strs = [""]
Output: [[""]]
```

### Solution

We start by creating a dictionary that maps a collection of letters to all of the words in the list that match as anagrams. We iterate through each word in the list and sort it. Then, we append that word to the list value for the key that matches the sorted version for the word. 

To finish, we return a list of the values in our map.

```
class Solution(object):
def groupAnagrams(self, strs):
    sorted_map = defaultdict(list)

    for word in strs:
        sorted_word = ''.join(sorted(word))
        sorted_map[sorted_word].append(word)

    return list(sorted_map.values())
```