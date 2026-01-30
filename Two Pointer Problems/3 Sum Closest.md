# 3 Sum Closest

## Problem Statement

Given an integer array nums of length n and an integer target, find three integers at distinct indices in nums such that the sum is closest to target.

Return the sum of the three integers.

You may assume that each input would have exactly one solution.

### Example 1

**Input:** `nums = [-1,2,1,-4]`, `target = 1`  
**Output:** `2`  
**Explanation:** The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

### Example 2

**Input:** `nums = [0,0,0]`, `target = 1`  
**Output:** `0`  
**Explanation:** The sum that is closest to the target is 0. (0 + 0 + 0 = 0).

## Constraints

- `3 <= nums.length <= 500`
- `-1000 <= nums[i] <= 1000`
- `-10^4 <= target <= 10^4`

## Solution

```python
class Solution:
    def threeSumClosest(self, nums: List[int], target: int) -> int:
        nums.sort()
        res = nums[0] + nums[1] + nums[2]
        n = len(nums)
        for i in range(n-2):
            left,right = i+1,n-1
            while left<right:
                total = nums[i]+nums[left]+nums[right]
                if abs(target - total)<abs(target-res):
                    res = total
                if total == target:
                    return target
                elif total<target:
                    left +=1
                else:
                    right-=1
        return res
```

## Explanation

The solution uses a two-pointer approach after sorting the array. We iterate through each element as the first number, then use two pointers to find the other two numbers that make the sum closest to the target.

For each fixed i, we set left = i+1 and right = n-1. We calculate the current sum and update the closest sum if it's closer to the target. Then, we move the pointers based on whether the current sum is less than or greater than the target.

### Step-by-Step Simulation for Example 2

**Input:** `nums = [0,0,0]`, `target = 1`  
**Output:** `0`

1. Sort nums: `[0,0,0]`
2. i = 0, left = 1, right = 2
3. current_sum = 0 + 0 + 0 = 0, abs(0 - 1) = 1, closest = 0
4. Since 0 < 1, left += 1, now left = 2, right = 2, loop ends
5. Return 0

The sum 0 is the closest to the target 1.
