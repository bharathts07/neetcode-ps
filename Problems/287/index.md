[287. Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return *this repeated number*.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

**Example 1:**

**Input:** nums = [1,3,4,2,2]
**Output:** 2

**Example 2:**

**Input:** nums = [3,1,3,4,2]
**Output:** 3

**Example 3:**

**Input:** nums = [3,3,3,3,3]
**Output:** 3

**Constraints:**

- `1 <= n <= 105`
- `nums.length == n + 1`
- `1 <= nums[i] <= n`
- All the integers in `nums` appear only **once** except for **precisely one integer** which appears **two or more** times.

**Follow up:**

- How can we prove that at least one duplicate number must exist in `nums`?
- Can you solve the problem in linear runtime complexity?

## Solution

```python

```

## Thoughts

Initially thoought this was a math problem requiring xor, didn;t know we could use the tortoise hare appraoch to this. Got help to solve this problem. Revise this again.

### Time Complexity

O(n), where n is the number of elements in the array. The hare moves at most 2n steps, and the tortoise moves at most n steps.

### Space Complexity

O(1), as we only use a few integer variables, which use constant space.
