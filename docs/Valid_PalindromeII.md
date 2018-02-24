## 680. Valid Palindrome II

Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome.

**Example 1:**

```
Input: "aba"
Output: True
```
**Example 2:**

```
Input: "abca"
Output: True
Explanation: You could delete the character 'c'.
```

### Code:

```java
class Solution {
    public boolean validPalindrome(String s) {
        int start = 0, end = s.length() - 1;
        while (start < end) {
            if (s.charAt(start) != s.charAt(end)) {
                return helper(s, start + 1, end) || helper(s, start, end - 1);
            }
            start++;
            end--;
        }
        return true;
    }
    
    public boolean helper(String s, int left, int right) {
        while (left < right) {
            if (s.charAt(left++) != s.charAt(right--)) return false;
        }
        return true;
    }
}
```

### 解题思路
* 用首尾指针法，遍历字符串；
* 遇到首尾指针所指元素不相同的情况，使用helper函数判断```(start+1, end)```或者```(start, end-1)```的情况是否为palindrome；
* helper函数同样使用首尾指针法判断字符串是否为palindrome。