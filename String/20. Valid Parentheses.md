## 20. Valid Parentheses
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

### Code:

```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for (Character c : s.toCharArray()) {
            if (c == '(' || c == '[' || c == '{') stack.push(c);
            else if (c == ')' && !stack.empty() && stack.peek() == '(') stack.pop();
            else if (c == ']' && !stack.empty() && stack.peek() == '[') stack.pop();
            else if (c == '}' && !stack.empty() && stack.peek() == '{') stack.pop();
            else return false;
        }
        return stack.empty();
    }
}
```

### 解题思路：
* 注意使用stack的先进后出特性，遍历字符串；
* 注意括号的对应关系，不是相等。
