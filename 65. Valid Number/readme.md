# 65. Valid Number

## Problem
- Validate if a given string is numeric.

> Some examples:
> 
> "0" => true
> 
> " 0.1 " => true
> 
> "abc" => false
> 
> "1 a" => false
> 
> "2e10" => true

- Note: It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.

## Solution
```python
class Solution(object):
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        try:
            float(s)
            return True
        except:
            return False
```

DFA solution, from [ref](https://discuss.leetcode.com/topic/30058/a-simple-solution-in-python-based-on-dfa):

![pic](pic.png)

```python
class Solution(object):
    def isNumber(self, s):
        """
        :type s: str
        :rtype: bool
        """
        states = [
            {' ': 0, 'sign': 1, 'digit': 2, '.': 3},
            {'digit': 2, '.': 3},
            {'digit': 2, '.': 4, 'e': 5, ' ': 8},
            {'digit': 4},
            {'digit': 4, 'e': 5, ' ': 8},
            {'sign': 6, 'digit': 7},
            {'digit': 7},
            {'digit': 7, ' ': 8},
            {' ': 8}
        ]
        cur = 0
        for c in s:
            if c == '+' or c == '-':
                c = 'sign'
            elif '0' <= c <= '9':
                c = 'digit'
            if c not in states[cur].keys():
                return False
            cur = states[cur][c]
        return cur in [2, 4, 7, 8]
```
