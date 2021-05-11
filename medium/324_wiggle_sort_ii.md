# Wiggle Sort II
https://leetcode.com/problems/wiggle-sort-ii/

## 1st Solution: Sorting
### Language: Python3
### Time Complexity: O(nlogn)

*   By partitioning the array with a median as a pivot, one will get a subarray *l* with all elements less than or equal to those of another subarray *r*.
*   And by placing elements from *l* into even indices, *r* into odd indices, the array will be wiggly sorted.
*   Now, to avoid duplicate numbers being adjacent to each other, one must reverse subarray *l* and *r* before placing them.

```python3
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = (len(nums) + 1) // 2
        nums.sort()
        l = nums[:n][::-1]
        r = nums[n:][::-1]
        for i in range(n):
            nums[2 * i] = l[i]
            if 2 * i + 1 < len(nums):
                nums[2 * i + 1] = r[i]
            
```

## 2nd Solution: Quick Select and virtual indexing
### Language: Python3
### Time Complexity: O(n) on average

With the objective to partition the array into two groups using median as a pivot, there is no need to sort the array. Instead, we can utilize quick selection algorithm to pick a median withing O(n) time complexity on average.

Then we need to devise a way to place elements in each group into the result array.
Consider the following methods.

1. Elements smaller than the median -> put into the last even index
2. Elements larger than the median -> put into the first odd index
3. The rest elements are to put into the remaining indices.

We can achieve this by using virtual indexing as follows.

* Old indices map to new indices by mapping the current index to the odd new index first, otherwise it maps to the first even index, and so on. 

Now, we create 3 variables: i, l, r; to keep track of current element, leftmost available odd index, rightmost available even index, respectively.

```
class Solution:
    def wiggleSort(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        n = len(nums)
        shuffle(nums)
        val = self.quickSelect(nums, n // 2)
        print(val)
        l, i, r = 0, 0, n - 1
        while i <= r:
            if nums[self.newIndex(i, n)] > val:
                self.swap(nums, self.newIndex(l, n), self.newIndex(i, n))
                l += 1
                i += 1
            elif nums[self.newIndex(i, n)] < val:
                self.swap(nums, self.newIndex(r, n), self.newIndex(i, n))
                r -= 1
            else:
                i += 1
                
    def swap(self, nums, a, b):
        nums[a], nums[b] = nums[b], nums[a]
                
    def newIndex(self, i, n):
        return (2 * i + 1) % (n | 1)
        
    def quickSelect(self, nums, k):
        l, r = 0, len(nums) - 1
        while l < r:
            pivot = self.partition(nums, l, r)
            if k > pivot:
                l = pivot + 1
            elif k < pivot:
                r = pivot - 1
            else:
                break
        return nums[k]
            
    def partition(self, nums, l, r):
        a = l
        for i in range(l + 1, r + 1):
            if nums[i] < nums[l]:
                a += 1
                self.swap(nums, i, a)
        self.swap(nums, a, l)
        return a
```
