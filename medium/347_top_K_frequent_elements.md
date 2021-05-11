# Top K Frequent ELements
https://leetcode.com/problems/top-k-frequent-elements/

## Solution: Bucket Sort
### Language: Python3
### Time Complexity: O(n) (linear in array size)

*   The idea is to create a bucket to store unique elements corresponding to each frequency.
*   Then, flatten the bucket to a single list.
*   Finally, return a list of K elements appearing most frequently (by reversing the bucket).

```python3
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        count = Counter(nums)
        freqs = [[] for i in range(len(nums) + 1)]
        for x, freq in count.items():
            freqs[freq].append(x)
        freqs = list(chain.from_iterable(freqs))
        return freqs[::-1][:k]
```

