class Solution:
    def isValid(self, s: str) -> bool:
        parens = []
        pairs = {')': '(', ']': '[', '}': '{'}
        for c in s:
            if c == ')' or c == ']' or c == '}':
                if len(parens) == 0 or pairs[c] != parens[-1]:
                    return False
                parens.pop()
            else:
                parens.append(c)
        return len(parens) == 0
