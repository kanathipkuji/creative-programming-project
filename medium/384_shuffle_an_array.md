# Shuffle an Array
https://leetcode.com/problems/shuffle-an-array/

### Solution: Straightforward Implementation with the help of methods in random.

```
class Solution:
    l = []
    def __init__(self, nums: List[int]):
        self.l = nums
        # self.randomL = nums

    def reset(self) -> List[int]:
        """
        Resets the array to its original configuration and return it.
        """
        return self.l

    def shuffle(self) -> List[int]:
        """
        Returns a random shuffling of the array.
        """
        return random.sample(self.l, len(self.l))
```

