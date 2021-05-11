# Flatten Nested List Iterator
https://leetcode.com/problems/flatten-nested-list-iterator/

## Solution: Recursion
### Language: Python3

*   Recursively call flatten() to ensure all nestedList get flattened.

```python3
# """
# This is the interface that allows for creating nested lists.
# You should not implement it, or speculate about its implementation
# """
#class NestedInteger:
#    def isInteger(self) -> bool:
#        """
#        @return True if this NestedInteger holds a single integer, rather than a nested list.
#        """
#
#    def getInteger(self) -> int:
#        """
#        @return the single integer that this NestedInteger holds, if it holds a single integer
#        Return None if this NestedInteger holds a nested list
#        """
#
#    def getList(self) -> [NestedInteger]:
#        """
#        @return the nested list that this NestedInteger holds, if it holds a nested list
#        Return None if this NestedInteger holds a single integer
#        """

class NestedIterator:
    def flatten(self, nestedList):
        for x in nestedList:
            if x.isInteger():
                self.flattenedList.append(x.getInteger())
            else:
                self.flatten(x.getList())    
    
    def __init__(self, nestedList: [NestedInteger]):
        self.idx = 0
        self.flattenedList = []
        self.flatten(nestedList)
        
    def next(self) -> int:
        ret = self.flattenedList[self.idx]
        self.idx += 1
        return ret
    
    def hasNext(self) -> bool:
         return self.idx < len(self.flattenedList)

# Your NestedIterator object will be instantiated and called as such:
# i, v = NestedIterator(nestedList), []
# while i.hasNext(): v.append(i.next())
```

