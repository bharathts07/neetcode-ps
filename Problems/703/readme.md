# [703. Kth Largest Element in a Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

**Example 1:**

**Input**
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
**Output**
[null, 4, 5, 5, 8, 8]

**Explanation**
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3); // return 4
kthLargest.add(5); // return 5
kthLargest.add(10); // return 5
kthLargest.add(9); // return 8
kthLargest.add(4); // return 8

**Constraints:**

- `1 <= k <= 104`
- `0 <= nums.length <= 104`
- `-104 <= nums[i] <= 104`
- `-104 <= val <= 104`
- At most `104` calls will be made to `add`.
- It is guaranteed that there will be at least `k` elements in the array when you search for the `kth` element.

## Solution

```python
class KthLargest:
    def __init__(self, k: int, nums: list[int]):
        self.heap = []
        self.k = k
        for num in nums:
            self.add(num)

    def add(self, val: int) -> int:
        if len(self.heap) < self.k:
            self.heap.append(val)
            self.heapify_up(len(self.heap) - 1)
        elif val > self.heap[0]:
            self.heap[0] = val
            self.heapify_down(0)
        return self.heap[0]

    def heapify_up(self, index: int):
        while index > 0:
            parent = (index - 1) // 2
            if self.heap[index] < self.heap[parent]:
                self.heap[index], self.heap[parent] = self.heap[parent], self.heap[index]
                index = parent
            else:
                break

    def heapify_down(self, index: int):
        while 2 * index + 1 < len(self.heap):
            left = 2 * index + 1
            right = 2 * index + 2
            smallest = index
            if self.heap[left] < self.heap[smallest]:
                smallest = left
            if right < len(self.heap) and self.heap[right] < self.heap[smallest]:
                smallest = right
            if smallest != index:
                self.heap[index], self.heap[smallest] = self.heap[smallest], self.heap[index]
                index = smallest
            else:
                break

# Your KthLargest object will be instantiated and called as such:
# obj = KthLargest(k, nums)
# param_1 = obj.add(val)



```

## Thoughts

### Time Complexity

Initialization (**init**): O(n log k), where n is the number of elements in nums.
Add (add): O(log k) for each add operation.

### Space Complexity

O(k) for the min heap.
