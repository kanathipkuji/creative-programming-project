```
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        first = nums[0]
        noSecond = True
        for num in nums:
            if num <= first:
                first = num
            elif noSecond or num <= second:
                second = num
                noSecond = False
            else:
                return True
        return False
```
