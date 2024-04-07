# [621. Task Scheduler](https://leetcode.com/problems/task-scheduler/)

You are given an array of CPU `tasks`, each represented by letters A to Z, and a cooling time, `n`. Each cycle or interval allows the completion of one task. Tasks can be completed in any order, but there's a constraint: **identical** tasks must be separated by at least `n` intervals due to cooling time.

​Return the *minimum number of intervals* required to complete all tasks.

**Example 1:**

**Input:** tasks = ["A","A","A","B","B","B"], n = 2

**Output:** 8

**Explanation:** A possible sequence is: A -> B -> idle -> A -> B -> idle -> A -> B.

After completing task A, you must wait two cycles before doing A again. The same applies to task B. In the 3rd interval, neither A nor B can be done, so you idle. By the 4th cycle, you can do A again as 2 intervals have passed.

**Example 2:**

**Input:** tasks = ["A","C","A","B","D","B"], n = 1

**Output:** 6

**Explanation:** A possible sequence is: A -> B -> C -> D -> A -> B.

With a cooling interval of 1, you can repeat a task after just one other task.

**Example 3:**

**Input:** tasks = ["A","A","A", "B","B","B"], n = 3

**Output:** 10

**Explanation:** A possible sequence is: A -> B -> idle -> idle -> A -> B -> idle -> idle -> A -> B.

There are only two types of tasks, A and B, which need to be separated by 3 intervals. This leads to idling twice between repetitions of these tasks.

## **Constraints:**

- `1 <= tasks.length <= 104`
- `tasks[i]` is an uppercase English letter.
- `0 <= n <= 100`

## Solution

```python
import heapq
from collections import deque

class Solution:
    def leastInterval(self, tasks: list[str], n: int) -> int:
        task_counts = {}
        for task in tasks:
            task_counts[task] = task_counts.get(task, 0) + 1

        # Create a max heap with negative counts to simulate a max heap using Python's min heap
        max_heap = [(-count, task) for task, count in task_counts.items()]
        heapq.heapify(max_heap)

        time = 0
        queue = deque()  # Queue to keep track of tasks in their cooling period

        while max_heap or queue:
            time += 1
            if max_heap:
                count, task = heapq.heappop(max_heap)
                count += 1  # Decrease the count as we've executed the task
                if count < 0:  # If there are still more instances of this task, add it to the queue
                    queue.append((count, task, time + n))

            if queue and queue[0][2] == time:  # Check if the task at the front of the queue can be executed
                heapq.heappush(max_heap, queue.popleft()[:2])

        return time

```

## Thoughts

Pretty hard problem, took help

### Time Complexity

The time complexity of this approach is O(n + m log m), where n is the number of tasks and m is the number of unique tasks.

- O(n) to count the occurrences of each task.
- Each iteration of the while loop takes O(log m) time due to the heap operations (heappop and heappush). In the worst case, there could be O(n) iterations if each task is executed in a separate time slot. However, in practice, the number of iterations is bounded by the number of unique tasks and the cooling interval, so it's more accurately O(m log m), where m is the number of unique tasks.

### Space Complexity

The space complexity of this approach is O(m), where m is the number of unique tasks.

- O(m) for the max heap to store the count of each unique task.
- O(m) for the queue to store tasks that are in their cooling period. In the worst case, all unique tasks could be in the queue at the same time.

Overall, the space complexity is dominated by the heap and the queue, so it's O(m).
