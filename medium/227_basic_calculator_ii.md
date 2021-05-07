# Basic Calculator II
https://leetcode.com/problems/basic-calculator-ii/

## 1st Solution: Evaluation of Infix Expression uisng Stacks  
### Language: C++

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

## 2nd Solution:  Optimized Version of 1st Solution
### Language: C++

Regarding the 1st solution, we multiply/divide the value on top of the stack until it reaches lower-precedent operators (+ or -) where we add/subtract the product/quotient from the stack. In this case, a stack is unnecessary since there are only 2 different operator precedences. Therefore, we can omit the stack.

Also, with the use of *stringstream* we eliminate redundant codes to extract the character (or integer).

```
class Solution {
    
public:
    int calculate(string s) {
        stringstream ss('+' + s + '+');
        int val, ans, x;
        char op;
        val = ans = 0;
        while (ss >> op) {
            if (op == '+' || op == '-') {
                ans += val;
                ss >> val;
                val *= op == '+' ? 1 : -1;
            } else if (op == '*') {
                ss >> x;
                val *= x;
            } else if (op == '/') {
                ss >> x;
                val /= x;
            }
        }
        return ans;
    }
};
```
