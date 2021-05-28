# Find Median from Data Stream
https://leetcode.com/problems/find-median-from-data-stream/

## Solution: Two heaps
### Language: C++

If the lower half of the sorted values are in maximum heap, and the upper half are in minimum heap, it is possible to find the medium by accessing the top value of both heaps.
In order to maintain the property by swapping elements from max heap that should belong to min heap, and keep the size to differ no more than 1.
Now, on each query, if the number of values so far is even, then we need to find an average of values from min heap and max heap. Otherwise, return the value from max heap.

```c++
class MedianFinder {
    priority_queue<int> maxHeap;
    priority_queue<int, vector<int>, greater<>> minHeap;
    int size;
    
public:
    /** initialize your data structure here. */
    MedianFinder() {
        size = 0;
    }
    
    void addNum(int num) {
        ++size;
        maxHeap.push(num);
        while (maxHeap.size() - minHeap.size() > 1) {
            minHeap.push(maxHeap.top());
            maxHeap.pop();
        }
        while (!maxHeap.empty() && !minHeap.empty() && minHeap.top() < maxHeap.top()) {
            int tmp = maxHeap.top();
            maxHeap.pop();
            maxHeap.push(minHeap.top());
            minHeap.pop();
            minHeap.push(tmp);
        }
    }
    
    double findMedian() {
        if (size < 1) {
            return 0;
        } else if (minHeap.empty()) {
            return maxHeap.top();
        } else if (maxHeap.empty()) {
            return minHeap.top();
        }
        if (size % 2) {
            return maxHeap.top();
        }
        return (maxHeap.top() + minHeap.top()) / 2.0;
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```
