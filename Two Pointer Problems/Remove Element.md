# Remove Element

## Problem Statement

Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.

Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:

Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.

Custom Judge:

The judge will test your solution with the following code:

```java
int[] nums = [...]; // Input array
int val = ...; // Value to remove
int[] expectedNums = [...]; // The expected answer with correct length.
                            // It is sorted with no values equaling val.

int k = removeElement(nums, val); // Calls your implementation

assert k == expectedNums.length;
sort(nums, 0, k); // Sort the first k elements of nums
for (int i = 0; i < actualLength; i++) {
    assert nums[i] == expectedNums[i];
}
```

If all assertions pass, then your solution will be accepted.

### Example 1

**Input:** `nums = [3,2,2,3]`, `val = 3`  
**Output:** `2, nums = [2,2,_,_]`  
**Explanation:** Your function should return k = 2, with the first two elements of nums being 2. It does not matter what you leave beyond the returned k (hence they are underscores).

### Example 2

**Input:** `nums = [0,1,2,2,3,0,4,2]`, `val = 2`  
**Output:** `5, nums = [0,1,4,0,3,_,_,_]`  
**Explanation:** Your function should return k = 5, with the first five elements of nums containing 0, 0, 1, 3, and 4. Note that the five elements can be returned in any order. It does not matter what you leave beyond the returned k (hence they are underscores).

## Constraints

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 50`
- `0 <= val <= 100`

## Solution

This problem can be solved using a two-pointer approach. We use two pointers: one to iterate through the array (`j`), and another to keep track of the position where we should place the next non-val element (`i`).

We initialize `i` to 0. As we iterate through the array with `j`, whenever we find an element that is not equal to `val`, we place it at position `i` and increment `i`. This way, all non-val elements are moved to the front of the array.

Let's walk through Example 1:

**Input:** `nums = [3,2,2,3]`, `val = 3`

- Start with `i = 0`, `j = 0`
- `nums[0] = 3` which equals `val`, so skip. `i` remains 0.
- `j = 1`, `nums[1] = 2` ≠ 3, so set `nums[0] = 2`, increment `i` to 1. Array: `[2,2,2,3]`
- `j = 2`, `nums[2] = 2` ≠ 3, so set `nums[1] = 2`, increment `i` to 2. Array: `[2,2,2,3]`
- `j = 3`, `nums[3] = 3` equals `val`, so skip. `i` remains 2.
- Return `i = 2`. The first 2 elements are `[2,2]`, which are the non-val elements.

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        i = 0
        for j in range(len(nums)):
            if nums[j] != val:
                nums[i] = nums[j]
                i += 1
        return i
```</content>
<parameter name="filePath">/workspaces/LeetCode-solutions/Two Pointer Problems/Remove Element.md