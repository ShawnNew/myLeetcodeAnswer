## 796. Rotate String

We are given two strings, A and B.

A shift on A consists of taking string A and moving the leftmost character to the rightmost position. For example, if A = 'abcde', then it will be 'bcdea' after one shift on A. Return True if and only if A can become B after some number of shifts on A.

```
Example 1:
Input: A = 'abcde', B = 'cdeab'
Output: true

Example 2:
Input: A = 'abcde', B = 'abced'
Output: false
```

**Note:**

A and B will have length at most 100.

### Code

```java
class Solution {
    public boolean rotateString(String A, String B) {
        return A.length() == B.length() && A.concat(A).contains(B);
    }
}
```

### 解题思路
这道题就足以见智商了:(。很明显我是智商不够的那个。将A字符串重复一次，如果满足题意，则B是新数组的一个子数组。