---
title: Two Sums
date: 2016-08-04 16:30:29
tags: Solutions
mathjax: true
description: The first problem in the Leetcode
---

[Question](https://leetcode.com/problems/two-sum/)
--------------

> Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
> You may assume that each input would have exactly one solution.
>
> >**Example:**
> >Given $nums = [2, 7, 11, 15], target = 9$,
> >Because $nums[0] + nums[1] = 2 + 7 = 9$,
> >return $[0, 1]$.

----------


 <i class="icon-road"></i> First Thought Solution
--------------

The brute force solution is very simple. Loop through each element $x$ and find if there is another $target - x$ existing.
```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
	}
}
```
Easy to see, the time complexity is $O(n^2)$ and the space complexity is $O(1)$.

<i class="icon-key"></i>Final Version
-------------------

Try to use HashMap to store the value and position pair. The benefit of using HashMap is that get and put are $O(1)$ operations[^1] which the whole time complexity is $O(n)$,  however the space complexity is $O(n)$.

```java
public class Solution {
	public int[] twoSum(int[] nums, int target) {
		Map<Integer, Integer> table = new HashMap<Integer, Integer>();
		for (int i=0; i < nums.length; ++i) {
			int reverseNum = target - nums[i];;
			if (table.containsKey(reverseNum)) {
				return new int[]{table.get(reverseNum), i};
			}
			table.put(nums[i], i);
		}
		return null;
	}
}
```

[^1]: The operation of HashMap in Java is not strictly $O(1)$. It really depends on how to select your hash code. You can see the details in this [article](http://stackoverflow.com/questions/4553624/hashmap-get-put-complexity).
