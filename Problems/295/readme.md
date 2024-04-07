# [295. Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/)

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.

- For example, for `arr = [2,3,4]`, the median is `3`.
- For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

- `MedianFinder()` initializes the `MedianFinder` object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far. Answers within `10-5` of the actual answer will be accepted.

**Example 1:**

**Input**
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
**Output**
[null, null, null, 1.5, null, 2.0]

**Explanation**
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1); // arr = [1]
medianFinder.addNum(2); // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3); // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0

## **Constraints:**

- `-10^5 <= num <= 10^5`
- There will be at least one element in the data structure before calling `findMedian`.
- At most `5 * 10^4` calls will be made to `addNum` and `findMedian`.

**Follow up:**

- If all integer numbers from the stream are in the range `[0, 100]`, how would you optimize your solution?
- If `99%` of all integer numbers from the stream are in the range `[0, 100]`, how would you optimize your solution?

## Solution

```python
import heapq

class MedianFinder:
    def __init__(self):
        self.max_heap = []  # Stores the smaller half
        self.min_heap = []  # Stores the larger half

    def addNum(self, num: int) -> None:
        if not self.max_heap or num <= -self.max_heap[0]:
            heapq.heappush(self.max_heap, -num)
        else:
            heapq.heappush(self.min_heap, num)

        # Rebalance the heaps
        if len(self.max_heap) > len(self.min_heap) + 1:
            heapq.heappush(self.min_heap, -heapq.heappop(self.max_heap))
        elif len(self.min_heap) > len(self.max_heap):
            heapq.heappush(self.max_heap, -heapq.heappop(self.min_heap))

    def findMedian(self) -> float:
        if len(self.max_heap) == len(self.min_heap):
            return (-self.max_heap[0] + self.min_heap[0]) / 2
        else:
            return -self.max_heap[0]

# Example usage
medianFinder = MedianFinder()
medianFinder.addNum(1)
medianFinder.addNum(2)
print(medianFinder.findMedian())  # Output: 1.5
medianFinder.addNum(3)
print(medianFinder.findMedian())  # Output: 2.0

```

## Thoughts

To maintain the median, we can use two heaps: a max heap to store the smaller half of the numbers and a min heap to store the larger half. This way, the median will either be the maximum of the max heap or the minimum of the min heap, or the average of the two for an even number of elements.

Here's how we can implement each method:

1. **`__init__`:** Initialize the max heap and min heap.
2. **`addNum`:** Add the number to the appropriate heap. If the number is less than or equal to the maximum of the max heap, add it to the max heap. Otherwise, add it to the min heap. Then, rebalance the heaps to ensure that the size difference between them is at most 1.
3. **`findMedian`:** If the heaps are of equal size, return the average of the maximum of the max heap and the minimum of the min heap. Otherwise, return the top of the larger heap.

### Question raised

1. If all integer numbers from the stream are in the range `[0, 100]`, we could use a fixed-size array to count the occurrences of each number. The median can be found by iterating over the array and counting the cumulative frequency until it reaches half the total number of elements.

2. If `99%` of all integer numbers from the stream are in the range `[0, 100]`, we could use a hybrid approach: use the fixed-size array for numbers in the range `[0, 100]` and use heaps for numbers outside this range. This way, we can quickly handle the common case while still being able to handle outliers.

### Time Complexity

- **`addNum`:** O(log n) due to the heap operations.
- **`findMedian`:** O(1) as we are just accessing the top of the heaps.

### Space Complexity

- O(n) for storing the numbers in the two heaps.
