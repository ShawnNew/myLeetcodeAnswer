## 32. Longest Valid Parentheses

Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.

For "(()", the longest valid parentheses substring is "()", which has length = 2.

Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.

### Code

```java
class Solution {
    public int longestValidParentheses(String s) {
        Stack<Integer> stack = new Stack<Integer>();
        int len = s.length(), longest = 0;
        
        //loop the string and stack invalidate index
        for (int i = 0; i < len; i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                if (!stack.empty()) {
                    if (s.charAt(stack.peek()) == '(') stack.pop();
                    else stack.push(i);
                } else stack.push(i);
            }
        }
        
        //loop the stack find the longest indice gap
        if (stack.empty()) longest = len;
        else {
            //valide indices are between the indices of stack(opposite of invalide)
            int valLeft = 0;   
            int valRight = len;
            while (!stack.empty()) {
                valLeft = stack.pop();
                longest = Math.max(longest, valRight-valLeft-1);
                valRight = valLeft;
            }
            longest = Math.max(longest, valRight);
        }
        
        return longest;
        
    }
}
```

### 解题思路

* 使用栈辅助解题，栈中存储的是不匹配的元素索引；
* 首先扫描字符串，在每一位遍历元素，如果出现'('，则将索引加入栈；
	* 如果出现')'，而且栈顶元素是'('，则说明找到了一个匹配，栈顶元素出栈；
	* 如果出现')'，但是栈顶元素不是'('，则说明不匹配，将索引入栈；
* 扫描完字符串之后，栈中的元素存储的是不匹配的元素的索引，所以匹配元素即为栈中相邻两元素之间的子字符串；
* 如果栈为空，说明元字符串全部匹配；否则则扫描栈，找到最长的索引间隔。