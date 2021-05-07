# Basic Calculator II
https://leetcode.com/problems/basic-calculator-ii/

## 1st Solution: Evaluation of Infix Expression uisng Stacks  
### Language: C++

*   Implement quick sort.
*   On each recursion of quick sort, if the pivot chosen is in the *k*-th position after partitioned, then it is the answer.
*   Because after partitioned, pivot will be moved to the right place if the array is all sorted. 

```
class Solution {
    int getPrecedence(char op) {
        switch(op) {
            case '*':
            case '/':
                return 2;
            case '+':
            case '-':
                return 1;
            default:
                return 0;
        }
    }
    
    bool hasHigherPrecedence(char op1, char op2) {
        return getPrecedence(op1) >= getPrecedence(op2);
    }
    
    int applyOp(int a, int b, char op) {
        switch(op) {
            case '*':
                return a * b;
            case '/':
                return a / b;
            case '+':
                 return a + b;
            case '-':
                 return a - b;
            default:
                return 0;
        }
    }
    
    void operate(stack<int>& ans, char op) {
        int b = ans.top();
        ans.pop();
        int a = ans.top();
        ans.pop();
        ans.push(applyOp(a, b, op));
    }
    
public:
    int calculate(string s) {
        int n = s.length();
        int val, a, b;
        char op;
        stack<int> ans, operators;
        for (int i = 0; i < n;) {
            if (isdigit(s[i])) {
                val = 0; 
                while (i < n && isdigit(s[i])) {
                    val *= 10;
                    val += s[i] - '0';
                    ++i;
                }
                ans.push(val);
            } else if (getPrecedence(s[i]) > 0) {
                op = s[i];
                while (!operators.empty() && hasHigherPrecedence(operators.top(), op)) {
                    operate(ans, operators.top());
                    operators.pop();
                }
                operators.push(op);
                ++i;
            } else {
                ++i;
            }
        }
        while (!operators.empty()) {
            operate(ans, operators.top());
            operators.pop();
        }
        return ans.top();
    }
};
```

