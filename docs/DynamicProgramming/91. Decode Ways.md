## 91. Decode Ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```
Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).

The number of ways decoding "12" is 2.

### Code:

```java
class Solution {
    public int numDecodings(String s) {
        int len = s.length();
        if (len == 0 || s == null) return 0;
        int[] dp = new int[len+1];
        dp[0] = 1;
        dp[1] = s.charAt(0) != '0' ? 1 : 0;
        for (int i = 2; i <= len; i++) {
            int first = Integer.valueOf(s.substring(i-1, i));
            int second = Integer.valueOf(s.substring(i-2, i));
            
            if (first > 0 && first <= 9) {
                dp[i] += dp[i-1];
            }
            if (second > 9 && second <= 26) {
                dp[i] += dp[i-2];
            }
        }
        return dp[len];
    }
}
```

### 解题思路
* 使用动态规划解决此题，dp数组存子问题的解；
* dp[0]表示对于空字符串的解码方式为1，dp[1]表示对于长度为一的字符串的解码方式；
* 然后遍历数组，检查两个字符和一个字符的解码方式，保存到dp数组中。