# [1899. Merge Triplets to Form Target Triplet](https://leetcode.com/problems/merge-triplets-to-form-target-triplet/)

A **triplet** is an array of three integers. You are given a 2D integer array `triplets`, where `triplets[i] = [ai, bi, ci]` describes the `ith` **triplet**. You are also given an integer array `target = [x, y, z]` that describes the **triplet** you want to obtain.

To obtain `target`, you may apply the following operation on `triplets` **any number** of times (possibly **zero**):

- Choose two indices (**0-indexed**) `i` and `j` (`i != j`) and **update** `triplets[j]` to become `[max(ai, aj), max(bi, bj), max(ci, cj)]`.
  - For example, if `triplets[i] = [2, 5, 3]` and `triplets[j] = [1, 7, 5]`, `triplets[j]` will be updated to `[max(2, 1), max(5, 7), max(3, 5)] = [2, 7, 5]`.

Return `true` *if it is possible to obtain the* `target` **_triplet_** `[x, y, z]` *as an **element** of* `triplets`*, or* `false` *otherwise*.

**Example 1:**

**Input:** triplets = [[2,5,3],[1,8,4],[1,7,5]], target = [2,7,5]
**Output:** true
**Explanation:** Perform the following operations:

- Choose the first and last triplets [[2,5,3],[1,8,4],[1,7,5]]. Update the last triplet to be [max(2,1), max(5,7), max(3,5)] = [2,7,5]. triplets = [[2,5,3],[1,8,4],[2,7,5]]
  The target triplet [2,7,5] is now an element of triplets.

**Example 2:**

**Input:** triplets = [[3,4,5],[4,5,6]], target = [3,2,5]
**Output:** false
**Explanation:** It is impossible to have [3,2,5] as an element because there is no 2 in any of the triplets.

**Example 3:**

**Input:** triplets = [[2,5,3],[2,3,4],[1,2,5],[5,2,3]], target = [5,5,5]
**Output:** true
**Explanation:** Perform the following operations:

- Choose the first and third triplets [[2,5,3],[2,3,4],[1,2,5],[5,2,3]]. Update the third triplet to be [max(2,1), max(5,2), max(3,5)] = [2,5,5]. triplets = [[2,5,3],[2,3,4],[2,5,5],[5,2,3]].
- Choose the third and fourth triplets [[2,5,3],[2,3,4],[2,5,5],[5,2,3]]. Update the fourth triplet to be [max(2,5), max(5,2), max(5,3)] = [5,5,5]. triplets = [[2,5,3],[2,3,4],[2,5,5],[5,5,5]].
  The target triplet [5,5,5] is now an element of triplets.

## **Constraints:**

- `1 <= triplets.length <= 10^5`
- `triplets[i].length == target.length == 3`
- `1 <= ai, bi, ci, x, y, z <= 1000`

## Solution

```python
class Solution:
    def mergeTriplets(self, triplets: List[List[int]], target: List[int]) -> bool:
        # Initialize three variables to track the maximum values of each index
        max_x, max_y, max_z = 0, 0, 0

        # Loop through each triplet
        for a, b, c in triplets:
            # Check if the current triplet can potentially contribute without exceeding the target
            if a <= target[0] and b <= target[1] and c <= target[2]:
                # Update the maximum values seen so far that are valid
                max_x = max(max_x, a)
                max_y = max(max_y, b)
                max_z = max(max_z, c)

        # Check if the collected maximum values meet or exceed the target values
        return max_x == target[0] and max_y == target[1] and max_z == target[2]

```

## Thoughts

Easier than the problem looks.

### Time Complexity

O(n), where n is the number of triplets. We only need one pass through the list of triplets.

### Space Complexity

O(1). We are using a constant amount of extra space regardless of the input size.
