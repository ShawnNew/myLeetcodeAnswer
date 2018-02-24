## 459. Repeated Substring Pattern

Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.
**Example 1:**

```
Input: "abab"

Output: True

Explanation: It's the substring "ab" twice.
```
**Example 2:**

```
Input: "aba"

Output: False
Example 3:
Input: "abcabcabcabc"

Output: True

Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)
```

### Code:

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        int len = s.length();
        for (int i = len / 2; i >= 1; --i) {
            if (len % i == 0) {
                int m = len / i;
                String subString = s.substring(0, i);
                StringBuilder sb = new StringBuilder();
                for (int k = 0; k < m; k++) {
                    sb.append(subString);
                }
                if (s.equalsIgnoreCase(sb.toString())) return true;
            }
        }
        return false;
    }
}
```

### 解题思路：
* 重复的子字符串必定小于字符串的一半，因此从字符串的一半长度开始寻找；
* 用0到i长度的substring构造新的字符串```s.substring(0,i);```，比较是否和原字符串一样，使用到```squalsIgnoreCase();```