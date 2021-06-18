# Valid Palindrome
https://leetcode.com/problems/valid-palindrome/

## Solution: Implement a stack that stores the minimum element
### Language: C++

When the method getMin() is called, we need to return the minimum element so far from all elements in a stack. The idea is to store that minimum element in every node on a stack, so that we can get the minimum element in O(1).

```C++
class MinStack {
public:
    /** initialize your data structure here. */
    struct Node {
        Node *prev;
        int min, val;
        Node(int x, Node* p=nullptr)
            :val(x), prev(p) {}
    };
    Node *curNode;
    
    MinStack() {
        curNode = nullptr;
    }
    
    void push(int x) {
        Node *p = new Node(x, curNode);
        if(curNode)
            p->min = min(x, curNode->min);
        else 
            p->min = x;
        curNode = p;
    }
    
    void pop() {
        curNode = curNode->prev;
    }
    
    int top() {
        return curNode->val;
    }
    
    int getMin() {
        return curNode->min;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

