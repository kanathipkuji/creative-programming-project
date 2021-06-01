# Evaluate Reverse Polish Notation
https://leetcode.com/problems/evaluate-reverse-polish-notation/

## Solution: Operand Stacking
### Language: Python3

Notice that all operations are operated on the latest 2 operands. Thus, if we utilize the stack data structure to store operands, and pop 2 operands from the stack when encountering an operator.
Then, we calculate the value and push the result to the stack.

```python3
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        operands = []
        
        def isOp(token):
            return token == '+' or token == '-' or token == '*' or token == '/'

        def operate(a, b, op):
            if op == '+': return a + b
            if op == '-': return a - b
            if op == '*': return a * b
            if op == '/': return int(a / b)
        
        def calculate(op):
            nonlocal operands
            b = operands[-1]
            operands.pop()
            a = operands[-1]
            operands.pop()
            operands.append(operate(a, b, op))
            
        for token in tokens:
            if not isOp(token):
                operands.append(int(token))
            else:
                calculate(token)
        
        return operands[0]
```

