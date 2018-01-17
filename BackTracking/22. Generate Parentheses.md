## 22. Generate Parentheses
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### Code

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> result = new ArrayList<String>();
        helper(result, "", 0, 0, n);
        return result;
    }
    
    public void helper(List<String> list, String s, int open, int close, int len) {
        if (s.length() == len*2) {
            list.add(s);
            return; 
        }
        if (open < len) helper(list, s+"(", open+1, close, len);
        if (close < open) helper(list, s+")", open, close+1, len);
    }
}
```

### 解题思路
* 使用递归的思路backtracking，可行解的条件是字符串的长度为len*2;
* 加（ 的条件是open（开括号的个数）小于len；
* 加 ）的条件是close（闭括号的个数）小于开括号的个数；
* 直观来讲，这道题的思路可以这样理解：有效的括号对必须以（）的形式成对出现，根据题设给出的n我们可以知道得到的有效字符串长度为2*n。字符串中（ 和 ）的个数满足上面两个条件所加的括号都是有效字符。