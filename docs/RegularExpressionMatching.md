## 10. Regular Expression Matching

Implement regular expression matching with support for '.' and '*'.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

### Code

```java
public class Solution {
    public boolean isMatch(String s, String p) {
        int sLen = s.length(), pLen = p.length();
        boolean[][] dp = new boolean[sLen+1][pLen+1];
        dp[0][0] = true;
        for (int i = 1; i <= pLen; i++) {
            if (p.charAt(i-1) == '*') dp[0][i] = dp[0][i-2];  //如果p中为*则比较p中前两位的字符
        }
        for (int i = 1; i <= sLen; i++) {
            for (int j = 1; j <= pLen; j++) {
                //如果遍历中s和p当前位完全匹配（相同或p中为.），则当前位dp为上一字符的dp
                if (match(s.charAt(i-1), p.charAt(j-1))) dp[i][j] = dp[i-1][j-1];  
                else {
                    if (p.charAt(j-1) == '*') {  //如果p的遍历位为*
                        dp[i][j] = dp[i][j-2];  //不使用*，即*匹配0个字符
                        if (match(s.charAt(i-1), p.charAt(j-2))) dp[i][j] |= dp[i-1][j];  //使用*，即找上一位匹配字符
                    }
                }
            }
        }
        return dp[sLen][pLen];
    }
    
    private boolean match(char c1, char r) {
        return c1 == r || r == '.';
    }
}
```

### 解题思路
* 使用动态规划解题，因为考虑到匹配的过程会需要使用前面的结果，所以应该使用一部分内存记录前面的结果，方便查询。
* 根据匹配规则，有如下三种情形：
	* 当遍历位中两元素完全匹配（相同，或p中出现‘.’），则当前结果为记录中的上一次匹配结果；
	* 如果遍历元素不能完全匹配，且p中出现'*'字符，则又分两种情况：
		* 使用*的匹配规则，即p的上一位与s的当前位匹配；
		* 不适用*的匹配规则，即p的上一位与s的当前位不匹配。
* 根据上述的三种情形遍历两个字符串，最后返回最终的匹配结果。