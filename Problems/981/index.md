# [981. Time Based Key-Value Store](https://leetcode.com/problems/time-based-key-value-store/)

Design a time-based key-value data structure that can store multiple values for the same key at different time stamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:

- `TimeMap()` Initializes the object of the data structure.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.

**Example 1:**

**Input**

`["TimeMap", "set", "get", "get", "set", "get", "get"]
[[], ["foo", "bar", 1], ["foo", 1], ["foo", 3], ["foo", "bar2", 4], ["foo", 4], ["foo", 5]]
`

**Output**

`[null, null, "bar", "bar", null, "bar2", "bar2"]`

**Explanation**

`TimeMap timeMap = new TimeMap();`

`timeMap.set("foo", "bar", 1); // store the key "foo" and
value "bar" along with timestamp = 1`

`timeMap.get("foo", 1); // return "bar"`

`timeMap.get("foo", 3); // return "bar", since there is no value corresponding to foo at timestamp 3 and timestamp 2, then the only value is at timestamp 1 is "bar".`

`timeMap.set("foo", "bar2", 4); // store the key "foo" and value "bar2" along with timestamp = 4.`

`timeMap.get("foo", 4); // return "bar2"`

`timeMap.get("foo", 5); // return "bar2"`

## **Constraints:**

- `1 <= key.length, value.length <= 100`
- `key` and `value` consist of lowercase English letters and digits.
- `1 <= timestamp <= 10^7`
- All the timestamps `timestamp` of `set` are strictly increasing.
- At most `2 * 10^5` calls will be made to `set` and `get`.

## Solution

```python
class TimeMap:

    def __init__(self):
        # Initialize a dictionary to store key -> list of (timestamp, value) pairs
        self.store = {}

    def set(self, key: str, value: str, timestamp: int) -> None:
        # If the key is not in the store, add it with an empty list
        if key not in self.store:
            self.store[key] = []
        # Append the (timestamp, value) pair to the list for this key
        self.store[key].append((timestamp, value))

    def get(self, key: str, timestamp: int) -> str:
        # If the key is not in the store, return an empty string
        if key not in self.store:
            return ""
        # Retrieve the list of (timestamp, value) pairs for this key
        pairs = self.store[key]
        # Perform a binary search to find the rightmost pair with timestamp <= given timestamp
        left, right = 0, len(pairs) - 1
        while left <= right:
            mid = (left + right) // 2
            if pairs[mid][0] <= timestamp:
                left = mid + 1
            else:
                right = mid - 1
        # Return the value associated with the found timestamp, or an empty string if not found
        return "" if right < 0 else pairs[right][1]

```

## Thoughts

The time complexity of the set method is O(1), as it simply appends a pair to a list. The time complexity of the get method is O(log n), where n is the number of pairs associated with the key, due to the binary search. The space complexity is O(m + n), where m is the number of unique keys and n is the total number of (timestamp, value) pairs stored in the TimeMap.
