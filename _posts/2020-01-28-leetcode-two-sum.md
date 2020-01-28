---
layout: post
title:  "LeetCode - 1. Two Sum"
author: Eujin Kim
categories: [ leetcode ]
image: 
tags: []
---

### Two Sum
```python
class Solution:
    def twoSum(self, nums, target):
        h={}
        for i, num in enumerate(nums):
            minus=target-num
            if minus not in h:
                h[num]=i
            else:
                return [h[minus],i]ar foo = 'bar';
                ```
