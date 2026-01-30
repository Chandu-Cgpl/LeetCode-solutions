# Trapping Rain Water

## Problem Statement

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

![Elevation Map](image.png)

### Example 1

**Input:** `height = [0,1,0,2,1,0,1,3,2,1,2,1]`  
**Output:** `6`  
**Explanation:** The above elevation map (black section) is represented by array `[0,1,0,2,1,0,1,3,2,1,2,1]`. In this case, 6 units of rain water (blue section) are being trapped.

### Example 2

**Input:** `height = [4,2,0,3,2,5]`  
**Output:** `9`

## Constraints

- `n == height.length`
- `1 <= n <= 2 * 10^4`
- `0 <= height[i] <= 10^5`

## Solution

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        left = 0
        n = len(height)
        right = n - 1
        water_level_left, water_level_right, water = 0, 0, 0
        while left < right:
            water_level_left = max(water_level_left, height[left])
            water_level_right = max(water_level_right, height[right])
            if water_level_left < water_level_right:
                water += water_level_left - height[left]
                print(water_level_right, water_level_left, water)
                left += 1
            else:
                water += water_level_right - height[right]
                print(water_level_right, water_level_left, water)
                right -= 1
        return water
```

## Explanation

The solution uses a two-pointer approach to efficiently compute the trapped rainwater. We initialize two pointers, `left` at the start and `right` at the end of the array. We also maintain two variables, `water_level_left` and `water_level_right`, to track the maximum height encountered from the left and right sides respectively.

In each iteration of the while loop (while `left < right`), we update the water levels by taking the maximum of the current water level and the height at the current pointers. Then, we compare the water levels:

- If `water_level_left` is less than `water_level_right`, it means the limiting factor for trapping water at the left pointer is the left water level. We add the difference between `water_level_left` and the current height at left to the total water, and move the left pointer to the right.
- Otherwise, we do the same for the right pointer.

This ensures that we always process the side with the smaller water level first, allowing us to calculate the trapped water correctly.

### Step-by-Step Simulation for Example 2

**Input:** `height = [4,2,0,3,2,5]`  
**Output:** `9`

Let's simulate the algorithm step by step:

1. **Initialize:** `left = 0`, `right = 5`, `water_level_left = 0`, `water_level_right = 0`, `water = 0`
2. **Iteration 1:** `water_level_left = max(0, 4) = 4`, `water_level_right = max(0, 5) = 5`  
   - Since `4 < 5`, `water += 4 - 4 = 0`, `left = 1`
3. **Iteration 2:** `water_level_left = max(4, 2) = 4`, `water_level_right = 5`  
   - Since `4 < 5`, `water += 4 - 2 = 2`, total `water = 2`, `left = 2`
4. **Iteration 3:** `water_level_left = max(4, 0) = 4`, `water_level_right = 5`  
   - Since `4 < 5`, `water += 4 - 0 = 4`, total `water = 6`, `left = 3`
5. **Iteration 4:** `water_level_left = max(4, 3) = 4`, `water_level_right = 5`  
   - Since `4 < 5`, `water += 4 - 3 = 1`, total `water = 7`, `left = 4`
6. **Iteration 5:** `water_level_left = max(4, 2) = 4`, `water_level_right = 5`  
   - Since `4 < 5`, `water += 4 - 2 = 2`, total `water = 9`, `left = 5`
7. **Loop ends** since `left == right`.

The total trapped water is **9 units**.